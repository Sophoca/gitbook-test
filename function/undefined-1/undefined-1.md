# Account Management

In the Account Management menu, you can view and manage all accounts registered in OwlDB.

{% hint style="info" %}
**Note**

The Account Management menu is accessible by Root only.
{% endhint %}

---

## Account List View

**[Account Management]** When you enter the menu, you can view the full list of accounts registered in OwlDB. You can filter by account status or search by ID, name, or email.

**Account Status**

| Account Status | Handling Method |
| --- | --- |
| Active | Normal account |
| Inactive | Account that has been deactivated |
| Account Requested | Account pending administrator approval |
| Deleted | Account that has been deleted |

---

## Account Creation

You can directly create a new Member account.

1. **[Account Management]** In the menu, **[Create]** Click the button.
2. Enter the account information (ID, name, password, etc.).
3. If necessary, you can also grant DB service access permissions at the same time.
4. **[Create]** Clicking the button completes the account creation.

Once the account is created, a permission grant notification is sent to the corresponding Member.

---

## Account Detail View and Edit

Clicking a user ID in the account list allows you to view the detailed information for that account. You can view and edit the detailed information of all accounts, including your own.

The items available for viewing are as follows.

- ID, name, role, email
- Granted DB service permissions
- Account status, creation date, last login date, modification date

To make edits, on the detail page, **[Edit]** Click the button.

---

## Account Creation Request Approval

When a user without an account requests account creation, the request appears in the **[Account Management]** menu `Account Requested` displayed with that status.

When Root changes the account to `Active` status, the account becomes active.

---

## Account Deletion

1. **[Account Management]** In the menu, select the account to delete.
2. **[Delete]** Click the button.
3. In the confirmation modal, **[Delete]** Clicking the button immediately blocks access to that account.

{% hint style="info" %}
**Note**

The ID of a deleted account cannot be reused. However, existing work history and logs are retained.

The Root account cannot be deleted.
{% endhint %}
