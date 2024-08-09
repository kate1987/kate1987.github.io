

# Set value

One trick in debugging is to set a variable to a different value, thereby forcing a specific code path. This can be particularly useful when patching broken behavior. 

!!! example
     If a feature fails and it's surrounded by an `if` statement, you might be able to disable that feature by forcing the value of a variable.

!!! warning
     This is an extremely risky action, and as such only users with the `ROLE_SET_VALUE` role can execute it. 

Once you've added the value, view the outuput [directly from the IDE](#view). 

--8<-- "ux-reference/plugin-intellij-prereq.md"


###### To add a set value action

1. Go to the line of your source code at which you'd like to set a value. 

2. Right-click to open the context menu:  

  ![Context Menu -half](assets/images/actions-menu.png)

3. Hover over [**Metrics**](#addaction) and then click **Set Value**.


4. Enter the relevant variable name for the left-side argument. The left hand side must be a variable in context and cannot be a method.

5. In the right-side field, enter the assigned value. Valid values include any Java expression, including a method invocation. 

6. Use `+` to add additional variables.

7. Click **Ok** to set the action.


!!! warning

     Quotas aren't imposed on set-value operations and as such the performance impact can be significant. 
	 


	 
--8<-- "ux-reference/update-actions.md"

## Configure piping

--8<-- "ux-reference/view-output.md"

## View values {#view}
--8<-- "ux-reference/view-logs.md"




