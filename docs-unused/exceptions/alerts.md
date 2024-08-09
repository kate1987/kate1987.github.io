# Alerts

Lightrun allows you to configure alerts about exceptions that are thrown in your applications.

Users with `ROLE_MANAGER` can configure alerts based on:

- weekly or daily notifications

- conditions:

  - every time there is a new error

  - errors that occur frequently

  - errors whose frequency has increased over time

--8<-- "ux-reference/manager-role-only.md"

###### To configure alerts

1. From a browser, go to your Lightrun account.

2. From the left menu, navigate to **Exceptions -> Email notifications**.

    The **Email notifications** window opens:

    ![Email Alerts -third](../assets/images/email-alerts.png)

3. To specify recipients for configured notifications, in the **Email Recipients** section enter a comma-separated list of addresses, similar to the following:

    ![Email Alerts -third](../assets/images/email-alerts-addresses.png)

4. Enable daily and weekly notifications, if relevant.

5. Scroll down to the **Get Notifications** section:

    ![Email Alerts -half](../assets/images/email-alerts-conditions.png)

    Enable the relevant options and configure their specific conditions as follows:

    - **A new error occurs** - no special conditions

    - **Error occurs frequently** - a notification is sent if, during the period indicated in the **times in** field, the error occurs more than the number of times indicated in the **Over** field.

    - **Frequency of specific exception increased** - a notification is sent if the error frequency increases by X during the time period Y.

6. Scroll to the bottom and click **Save**.
