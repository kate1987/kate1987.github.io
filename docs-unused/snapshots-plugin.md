# Snapshots

A snapshot is a one-time "breakpoint" that doesn't block your code from running; as opposed to a traditional breakpoint, snapshots collect the stack trace and variables without interrupting the application at all.

Once you've added the snapshot, view the output [directly from the IDE](#view).

--8<-- "ux-reference/plugin-intellij-prereq.md"

###### To add a snapshot

1. Go to the line of your source code at which you'd like to insert the snapshot.

2. Right-click to open the context menu:  

    ![Context Menu -half](assets/images/context-menu.png)

3. Select **Snapshot**:

    The **Create Snapshot** dialog opens: 
	
	![Adding a Snapshot](assets/images/add-snapshot.png)

4. Complete the fields in the dialog as follows:

  -   **Agent**
      
      --8<-- "ux-reference/pick-agent.md"

  -   **File**
      
      --8<-- "ux-reference/file.md"

  -   **Expression**
      
      --8<-- "ux-reference/expression.md"

  -   **Condition**
      
    --8<-- "ux-reference/configure-condition.md"

5. Click **Advanced** to configure the following additional fields:

  - **Max Hit Count**
  
    the maximum number of times the snapshot should be taken during the lifetime of the action; default == 1.
  
  - **Ignore quotas** 
  
    --8<-- "ux-reference/ignore-quotas.md"

  - **Expiry**
  
    --8<-- "ux-reference/expiry.md"

6. Click **OK** to add the snapshot. A marker is also added to the area above the line:

    The snapshot is added and displayed in the bottom sidebar:

    ![Snapshot Result](assets/images/intellij-snapshots.gif)

    An icon is added to the margins of the code on the line where it was added:

    ![Snapshot Inserted](assets/images/snapshot-edit.png)

7. Right-click ![Snapshot icon -icon](assets/images/snapshot-gutter.png) from the gutter marker to delete or edit the configuration.

--8<-- "ux-reference/update-actions.md"

### Snapshot data - view the stacktrace {#view}

Every time you add a snapshot to the code, it appears in the bottom sidebar of IntelliJ in the Lightrun Snapshots tab. The layout of the data that prints out is similar to the debugger interface, designed to be familiar to you.

![Stacktrace in plugin -three](assets/images/intellij-snapshots.gif)

Find these details in the Lightrun Snapshots view:

The name that was assigned to the snapshot when it was added appears at the top of the sidebar.
The left column lists all of the stack trace frames from the relevant snapshot.
Click the row of a specific frame to view the variables related to the exception that was thrown.

Viewing snapshot data in the Management Portal is further detailed [here](snapshots.md){:target="_blank"}
