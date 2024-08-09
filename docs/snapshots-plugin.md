# Snapshots

## Overview

A snapshot is a one-time "breakpoint" that doesn't block your code from running. As opposed to a traditional breakpoint, snapshots collect the stack trace and variables without interrupting the application at all.

From your JetBrains IDE, you can:

- [To add a snapshot](https://docs.lightrun.com/snapshots-plugin/#add)
- [To view snapshot data](https://docs.lightrun.com/snapshots-plugin/#view)
- [To edit and delete a snapshot](https://docs.lightrun.com/snapshots-plugin/#edit)
- [To copy and paste a Lightrun snapshot](https://docs.lightrun.com/snapshots-plugin/#copy)

--8<-- "ux-reference/plugin-intellij-prereq.md"

## To add a snapshot {#add}

1. Go to the line of your source code at which you'd like to insert the snapshot.

2. Right-click to open the context menu:  

    ![Context Menu -half](/assets/images/context-menu.png)

3. Select **Snapshot**:

    The **Create Snapshot** dialog should appear similar to the following image. 
	
	![Adding a Snapshot -half](/assets/images/add-snapshot1.png)

	The following table describes the present fields.

	| Field | Description    |
	|--------|----------------|
	| **Source** | From the available options in the dropdown list, bind the action to a specific agent, tag, or custom source. <br>Click *Create Custom Source* to create a new custom source.         |
	| **Filename & Line**   |  The source code file and line of code into which you're inserting the snapshot. The default path is to the source code file from which you're currently working.              |
	| **Expression** | Variables or method results to be displayed in the snapshot stack trace. Click + to enter additional expressions.           |
	| **Condition**  |  The condition of an `if` statement, used to limit the execution of the action. For example, The condition `myVar % 7 == 0` limits the action (log, snapshot, metric) output so that it only prints for variables that are divisible by 7.          |
	| **Max Hit Count** | the maximum number of times the snapshot should be taken during the lifetime of the action; default == 1.        |

4. Click **Advanced** to configure the following additional fields:

	| Field | Description    |
	|--------|----------------|
	| **Ignore quotas** | The maximum number of times the snapshot should be taken during the lifetime of the action; default == 1. |
	| **Expiry** | The time after which the action ceases to track code behavior and is automatically disabled; default = 1 hour. |

6. Click **Save** to add the snapshot.

	A snapshot marker ![Snapshot icon -icon](/assets/images/snapshot-gutter.png) should appear next to the selected code line in your Jetbrains code editor.

Once a snapshot hit has been captured, you will be notified directly in your IDE. 

![Snapshot icon -ten](/assets/images/snapshot-taken.png)

## To view snapshot data {#view}

Once a snapshot hit has been captured, you can view the snapshot data directly in your IDE or in the Lightrun management portal in your browser. Click [here](/snapshots/) for more information on how to view your snapshot data in the Lightrun management portal.

To view snapshot data in your IDE, click on the snapshot marker ![Snapshot icon -icon](/assets/images/snapshot-gutter.png) to open the Lightrun Snapshot window or click on **Lightrun Snapshots** in the bottom part of your IDE.

The Lightrun Snapshot tool window should appear similar to the following image.

![Snapshot -half](/assets/images/snapshot-02.png)


Click on a snapshot to populate the **Captured Hits**, **Frames**, and **Variables** section with its data. 

![Snapshot -half](/assets/images/snapshot-01.png)

See [JetBrains plugin quick tour](/getting-around/#snapshot) to learn more about the Lightrun Snapshot tool window.

## To edit and delete a snapshot {#edit}

1. Right-click on the snapshot marker ![Snapshot icon -icon](/assets/images/snapshot-gutter.png) on the snapshot code line.
2. Click **Delete** to delete the snapshot.
3. Click **Edit** to edit the snapshot configuration.

## To copy and paste a Lightrun snapshot {#copy}
 
This procedure allows you to easily reuse existing snapshots in multiple locations within your code.  Note that the snapshot is saved in the clipboard and can be pasted multiple times.

1. Right-click on the snapshot marker ![Snapshot icon -icon](/assets/images/snapshot-gutter.png) on the snapshot code line that you would like to copy.
2. Click **Copy** to copy the snapshot settings.
   
   ![Snapshot copy -half](/assets/images/jetbrains-copy-snapshot.png)

   The **Insert a Counter** window opens with the copied metrics.

3. Update with a new counter name and click **OK**.

4. Go to the line of your target source code at which you'd like to insert the copied snapshot, right-click and click **Paste Snapshot**.
   
   ![Snapshot paste -half](/assets/images/jetbrains-paste-snapshot.png)

