A snapshot is a one-time "breakpoint" that doesn't block your code from running. As opposed to a traditional breakpoint, snapshots collect the stack trace and variables without interrupting the application at all.

From your JetBrains IDE, you can:

- [Add a snapshot](#add)
- [View snapshot data](#view)
- [Edit snapshot configuration](#edit)
- [Delete a snapshot](#delete)


--8<-- "ux-reference/plugin-intellij-prereq.md"

###### To add a snapshot {#add}

1. Go to the line of your source code at which you'd like to insert the snapshot.

2. Right-click to open the context menu:  

    ![Context Menu -half](assets/images/context-menu.png)

3. Select **Snapshot**:

    The **Create Snapshot** dialog opens: 
	
	![Adding a Snapshot -half](assets/images/add-snapshot1.png)

	The following table describes the present fields.

	| Fields | Description    |
	|--------|----------------|
	| **Target** | Bind the snapshot to a specific tag or agent from the available options in the dropdown list.               |
	| **File**   |  The source code file and line of code into which you're inserting the snapshot. The default path is to the source code file from which you're currently working.              |
	| **Expression** | Variables or method results to be displayed in the snapshot stack trace. Click + to enter additional expressions.           |
	| **Condition**  |  The condition of an `if` statement, used to limit the execution of the action. For example, The condition `myVar % 7 == 0` limits the action (log, snapshot, metric) output so that it only prints for variables that are divisible by 7.          |
	| **Max Hit Count** | the maximum number of times the snapshot should be taken during the lifetime of the action; default == 1.        |

4. Click **Advanced** to configure the following additional fields:

	| Fields | Description    |
	|--------|----------------|
	| **Ignore quotas** | The maximum number of times the snapshot should be taken during the lifetime of the action; default == 1. |
	| **Expiry** | The time after which the action ceases to track code behavior and is automatically disabled; default = 1 hour. |

6. Click **OK** to add the snapshot. A marker is also added to the area above the line:

    The snapshot is added and displayed in the bottom sidebar:

    ![Snapshot Result](assets/images/intellij-snapshots.gif)

    An icon is added to the margins of the code on the line where it was added:

    ![Snapshot Inserted](assets/images/snapshot-edit.png)

7. Right-click ![Snapshot icon -icon](assets/images/snapshot-gutter.png) from the gutter marker to delete or edit the configuration.

###### To view snapshot data {#view}

###### To edit a snapshot configuration {#edit}

###### To delete a snapshot {#delete}