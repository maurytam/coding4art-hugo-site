---
title: The Interface Segregation Principle (ISP)
author: mtammacco
type: post
date: 2010-12-07T14:38:18+00:00
url: /archive/2010/12/07/the-interface-segregation-principle-isp.aspx
categories:
  - SOLID Principles

---
The Interface Segregation Principle (ISP) is another principle about OOD.

It simply states that:

<p align="center">
  <strong><em>“CLIENTS SHOULD NOT BE FORCED TO DEPEND UPON INTERFACES<br /> THAT THEY DON’T USE”</em></strong>
</p>

If we return back to the <a href="http://www.coding4art.com/archive/2010/11/22/the-first-solid-principle-srp.aspx" target="_blank" rel="noopener">first OOD principle, the Single Responsibility Principle</a>, it can be said that this principle should also apply to interfaces or to abstract class, in addition to the concrete classes.

Therefore, one interface should mean one responsibility, without creating the so-called “**fat interfaces**”, i.e. interfaces that contain too many methods/properties that relate to more than 1 responsibility.

To find an example of violation of this principle does not need to go too far, just peek inside the .Net framework itself .

If we take a look inside the abstract class MembershipProvider, which is the class which all providers, default and custom,  inherit from, we’ll be looking at 28 abstract methods, which must be provide an implementation in case of creation of custom membership provider.

<pre class="brush: csharp; title: ; notranslate" title="">public abstract void Initialize(string name,
      NameValueCollection config)
  public abstract string ApplicationName { get; set; }
  public abstract bool EnablePasswordReset { get; }
  public abstract bool EnablePasswordRetrieval { get; }
  public abstract bool RequiresQuestionAndAnswer { get; }
  public abstract bool RequiresUniqueEmail { get; }
  public abstract int MaxInvalidPasswordAttempts { get; }
  public abstract int PasswordAttemptWindow { get; }
  public abstract MembershipPasswordFormat PasswordFormat { get; }
  public abstract int MinRequiredNonAlphanumericCharacters { get; }
  public abstract int MinRequiredPasswordLength { get; }
  public abstract string PasswordStrengthRegularExpression { get; }
  public abstract bool ChangePassword(string username,
      string oldPwd, string newPwd)
  public abstract bool ChangePasswordQuestionAndAnswer(
      string username, string password, string newPwdQuestion,
      string newPwdAnswer)
  public abstract MembershipUser CreateUser(string username,
      string password, string email, string passwordQuestion,
      string passwordAnswer, bool isApproved, object
      providerUserKey, out MembershipCreateStatus status)
  public abstract bool DeleteUser(string username,
      bool deleteAllRelatedData)
  public abstract MembershipUserCollection GetAllUsers(int  
     pageIndex,
     int pageSize, out int totalRecords)
  public abstract int GetNumberOfUsersOnline()
  public abstract string GetPassword(string username, string answer)
  public abstract MembershipUser GetUser(string username,
      bool userIsOnline)
  public abstract MembershipUser GetUser(object providerUserKey,
      bool userIsOnline)
  public abstract bool UnlockUser(string username)
  public abstract string GetUserNameByEmail(string email)
  public abstract string ResetPassword(string username,
      string answer)
  public abstract void UpdateUser(MembershipUser user)
  public abstract bool ValidateUser(string username,
      string password)
  public abstract MembershipUserCollection FindUsersByName(
      string usernameToMatch, int pageIndex, int pageSize,
      out int totalRecords)

</pre>

This methods has to do with authentication, persistence, retrieve of user based on various criteria, password management, and so on.

All these abstract methods must be implemented even if the client code that uses the feature is only interested in some of these aspects mentioned above.

In this way, the methods that you do not care end up being defined as follows:

<pre class="brush: csharp; title: ; notranslate" title="">public override int GetNumberOfUsersOnline()
{
    throw new NotImplementedException();
}

</pre>

This approach has several problems, including:

  * Indirect and especially useless  coupling between clients that use the functionality. If additional functionality is required, all clients must be modified, even those not interested in new features;
  * Clients are misled because some methods explicitly raise an exception;
  * Code maintenance is more difficult;