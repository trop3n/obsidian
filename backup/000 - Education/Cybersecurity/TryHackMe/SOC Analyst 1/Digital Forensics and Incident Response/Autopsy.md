Autopsy is an open-source and powerful digital forensics platform. Several features within Autopsy have been developed by the Department of Homeland Security Science and Technology funding. You can read more about this [here](https://www.dhs.gov/science-and-technology/news/2017/12/12/snapshot-st-enhancing-autopsy-digital-forensics-tool). 

[**The official description**](https://www.autopsy.com/): "_Autopsy is the premier open source forensics platform which is fast, easy-to-use, and capable of analyzing all types of mobile devices and digital media. Its plug-in architecture enables extensibility from community-developed or custom-built modules. Autopsy evolves to meet the needs of hundreds of thousands of professionals in law enforcement, national security, litigation support, and corporate investigation._"

# Workflow Overview

Before diving into Autopsy and analyzing data, there are a few steps to perform; such as identifying the data source and what Autopsy actions to perform with the data source. 

## Basic Workflow:

1. Create/Open the case for the data source you will investigate
2. Select the data source you wish to analyze
3. Configure the ingest modules to extract specific artifacts from the data source
4. Review the artifacts extracted by the ingest modules
5. Create the report

## Case Analysis | Create a New Case

To prepare a new case investigation, you need to create a case file from the data source. When you start autopsy, there will be three options. You can create a new case file using the **"New Case"** option. Once you click on the "New Case" option, the **Case Information** menu opens, where information about the case is populated.

- **Case Name**: The name you wish to give to the case
- **Base Directory**: The root directory that will store all the files specific to the case (the full path will be displayed)
- **Case Type**: Specify whether this case will be local (`Single-User`) or hosted on a server where multiple analysts can review (`Multi-User`).

**Note**: In this room the focus is on **single user**. Also, the room doesn't simulate a new case creation, and the given VM has a sample case file for practice covered Autopsy features. 

The following screen is titled "**Optional Information**" and can be left blank for our purposes. In an actual forensic environment, you should fill out this information. Once you click on "Finish", Autopsy will create a new file from the given data source.

![](https://i.imgur.com/G4iWv8M.png)

## Case Analysis | Open an Existing Case

Autopsy can also open prebuilt case files. Note that supported data sources are discussed in the next task. This part aims to show how to create/open case files with Autopsy.

**Note**: Autopsy case file have an `.aut` file extension.

**In this room, you will import a case**. To open a case, select the "Open Case" option. Navigate to the case folder (located on the desktop) and select the `.aut` file you wish to open. Next, Autopsy will process the case files and open the case. You can identify the name of the case at the top left corner of the Autopsy window. In the image below, the name of the case is **Sample Case**.

![](https://i.imgur.com/FYMasUR.png)

**Note**: A warning box will appear if Autopsy cannot locate the disk image. At this point, you can point to the location of the disk image it's attempting to find, or you can click **NO**; you can still analyze the data from the Autopsy case.

![](https://i.imgur.com/a3IxfbG.png)

# Data Sources

Autopsy can analyze multiple disk image formats. Before diving into the data analysis step, let's briefly cover the different data sources Autopsy can analyze. You can add data sources by using the "**Add Data Source**" button. Available options are shown in the picture below. 

**We will focus primarily on the Disk Image or VM File option in this room**.

Supported Disk Image formats:

- **Raw Single** (For example: *.img, *.dd, *.raw, *.bin)
- **Raw Split** (For example: *.001, *.002, *.aa, *.ab, etc)
- **EnCase** (For example: *.e01, *.e02, etc)
- **Virtual Machines** (For example: *.vmdk, *.vhd)

If there are multiple image files (i.e. E01, E02, E03, etc.) Autopsy only needs you to point to the first image file, and Autopsy will handle the rest. 

**Note**: Refer to the Autopsy [documentation](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/ds_page.html) to understand the other data sources that can be added to a case.
# Ingest Modules

Essentially **Ingest Modules** are Autopsy plug-ins. Each Ingest Module is designed to analyze and retrieve specific data from the drive. You can configure Autopsy to run specific modules during the source-adding stage or later by choosing the target data source available on the dashboard.

By default, the Ingest Modules are configured to run on **All Files, Directories and Unallocated Space**. You can change this setting during the module selecting step. You can track the process with the bar appearing in the lower right corner. 

The below screenshots simulate mentioned two different approaches to using ingest modules. Note that using ingest modules requires time to implement. Therefore, we will not be covering ingest modules in this room. 

Note: Autopsy adds metadata about files to the local database, not the actual file contents.
## Configuring Ingest Modules While Adding Data Sources

![](https://i.imgur.com/q1ftVbd.png)

## Using Ingest Modules after Adding Data Sources

1. Open the "Run Ingest Modules" menu by right-clicking on the data source.
2. Choose the modules to implement and click on the finish button.
3. Track the progress of implementation

![](https://i.imgur.com/ezmeFWT.png)

The results of any Ingest Module you select to run against a data source will populate the Results node in the Tree view, which is the left pane of the Autopsy user interface. Below is an example of using the `Interesting Files Folder` ingest module. Note that the results depend on the dataset. If you choose a module to retrieve specific data that is unavailable in the drive, there will be no results.

![](https://i.imgur.com/94eNPaF.png)

Drawing the attention back to the Configure Ingest Modules window, notice that some Ingest Modules have **per-run settings** and some do not. For example, the **Keyword Search** Ingest Module does not have per-run settings. In contrast, the **Interesting files Finder** Ingest Module does. The yellow triangle represents the `per run settings option`.

As ingest modules run, alerts may appear in the `Ingest Inbox`. Below is an example of the Ingest Inbox after a few ingest modules have completed running. 

![](https://i.imgur.com/KhdScPr.png)

To learn more about Ingest Modules, read Autopsy documentation [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/ingest_page.html).

# The User Interface I

Let's look at the autopsy interface, which is comprised of 5 primary areas:
## Tree Viewer

The **Tree Viewer** has **five top-level nodes**:

- **Data Sources**: all the data will be organized as you would typically see it in a normal Windows File Explorer.
- **Views**: files will be organized based on file types, MIME types, file size, etc.
- **Results**: as mentioned earlier, this is where the results from Ingest Modules will appear. 
- **Tags**: will display files and/or results that have been tagged (read more about tagging [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/tagging_page.html))
- **Reports**: will display reports either generated by modules or the analyst (read more about reporting [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/reporting_page.html)).

Refer to the autopsy documentation on the **Tree Viewer** for more information [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/tree_viewer_page.html).
## Result Viewer

**Note**: Don't confuse the results node (from the Tree Viewer) with the Result Viewer.

When a volume, file, folder, etc. is selected from the Tree Viewer, additional information about the selected item is displayed in the Result Viewer. For example, the Sample case's data source is selected, and now additional information is visible in the Results Viewer.

![](https://i.imgur.com/NuHCbnk.png)

If a volume is selected, the Result Viewer's information will change to reflect the information in the local database for the selected volume. 

![](https://i.imgur.com/glsrRMz.png)

Notice that the Result Viewer pane has three tabs: **Table, Thumbnail and Summary**. The above screenshots reflect the information displayed in the Table tab. The Thumbnail tab works best with image or video files. If the view of the above data is changed from Table to Thumbnail, not much information will be displayed. See below.

![](https://i.imgur.com/M59IfDU.png)

Volume nodes can be expanded, and an analyst can navigate the volume's contents like a typical Windows system.

![FuAqW9N.png](https://i.imgur.com/FuAqW9N.png)

In the views tree node, files are categorized by File Types - **By Extension, By MIME Type, Deleted Files, and by File Size** 

![](https://i.imgur.com/8kJRslM.png)

> [!TIP]
> **Tip**: when it comes to **File Types**, pay attention to this section. An adversary *can rename a file with a misleading file extension*. So the file will be 'miscategorized' appropriately by **MIME type**. Expand `by file extension` and more children nodes appear, categorizing the files even further. 

![](https://i.imgur.com/zkzM8NO.png)

Refer to the Autopsy documentation on the **Result Viewer** for more information [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/result_viewer_page.html).
## Contents Viewer

From the Table tab in the Result viewer, if you click any folder/file, additional information is displayed in the Contents Viewer pane.

![](https://i.imgur.com/IjFzPNO.png)

In the given image, three columns might not be quickly understood what they represent.

- **S = Score**

The **Score** will show a red exclamation point for a folder/file marked/tagged as notable and a yellow triangle pointing downward for a folder/file marked/tagged as suspicious. These items can be marked/tagged by an Ingest Module or the analyst.

- **C = Comment**

If a yellow page is visible in the Comment column, it will indicate that there is a comment for the folder/file. 

- **O = Occurrence**

In a nutshell, this column will indicate how many times this file/folder has been seen in past cases (this will require the [Central Repository](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/central_repo_page.html))

Refer to the Autopsy documentation on the Contents Viewer for more information [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/content_viewer_page.html).
## Keyword Search

At the top right, you will find **Keyword Lists** and **Keyword Search**. With `keyword search`, an analyst can perform an AD-HOC keyword search.

![](https://i.imgur.com/ap0usI8.png)

In the image above, the analyst searches for the word 'secret'. Below are the attached search results.

![](https://i.imgur.com/STCoLG1.png)

Refer to the Autopsy [documentation](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/ad_hoc_keyword_search_page.html) for more information on performing keyword searches with either option.

## Status Area

Lastly, the **Status Area** is at the bottom right. When Ingest Modules run, a progress bar (along with the percentage completed) will be displayed in this area. More detailed information regarding the ingest modules is provided if you click the bar. 

If the `X` (directly next to the progress bar) is clicked, a prompt will appear confirming if you wish to end/cancel the Ingest Modules. 

Refer to the Autopsy documentation on the UI overview [here](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/uilayout_page.html).

# The User Interface II

Let's look at where we can find summarized info with ease. Summarized info can help analysts decide where to focus by evaluating available artifacts. It is suggested to view the summary of the data sources before starting an investigation. Therefore you can have a general idea about the system and artefacts.
## Data Sources Summary

The **Data Sources Summary** provides summarized info in nine different categories. Note that this is an overview of the total findings. If you want to dive deep into the findings and look for a specific artefact, you need to *analyze each module separately* using the **Result Viewer** shown the previous task.

![](https://i.imgur.com/Sioeq6n.png)

## Generate Report

You can generate a report of your findings in multiple formats, enabling you to create data sheets for your investigation case. The report provides all information listed under the "Result Viewer" pane. Reports can help you to re-investigate findings after finishing the live investigation. **However, reports don't have additional search options, so you must manually find artefacts for the event of interest.**

**Tip**: The Autopsy tool can be heavy for systems with low resources. Therefore completing an investigation with Autopsy on low resources can be slow and painful. Especially browsing long results might end up with a system freeze. You can avoid that situation by using reports. You can use tool for parsing the data and generating the report, then continue to analyze through the generated report without a need for Autopsy. Note that it is much easier to conduct and manage an investigation with the GUI.

You can use the **Generate Report** option to create reports. The steps are shown below.

![](https://i.imgur.com/V0y7kvu.png)

> Once you choose your report format and scope, Autopsy will generate the report. You can click on the "HTML Report" section to view the report on your browser. Reports contain all of the "Result Viewer" pane results on the left side.

![](https://i.imgur.com/fM7nnLp.png)

# Data Analysis

**Mini Scenario**: An employee was suspected of leaking company data. A disk image was retrieved from the machine. You were assigned to perform the initial analysis. Further action will be determined based on the initial findings.

**Reminder**: Since the actual disk image is not in the Attached VM, certain Autopsy sections will not display any actual data, only the metadata for that row within the local database. You can click when you're notified about the '**Missing Image**.' Additionally, you do **not** need to run any ingest modules in this exercise.

# Visualization Tools

You may have noticed that other parts of the user interface weren't discussed as of yet.

Please refer to the Autopsy documentation for the following visualisation tool:

- **Images/Videos:** [http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/image_gallery_page.html](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/image_gallery_page.html)
- **Communications:** [http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/communications_page.html](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/communications_page.html)
- **Timeline:** [http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/timeline_page.html](http://sleuthkit.org/autopsy/docs/user-docs/4.12.0/timeline_page.html)

**Note**: Within the attached VM, you will **NOT** be able to practice with some of the visualisation tools, except for **Timeline**. Below is a screenshot of the **Timeline**.

![](https://i.imgur.com/hmB6C2W.png)

**The Timeline tool is composed of three areas:**

1. **Filters:** Narrow the events displayed based on the filter criteria
2. **Events:** The events are displayed here based on the **View Mode**
3. **Files/Contents:** Additional information on the event(s) is displayed in this area

**There are three view modes:**

1. **Counts:** The number of events is displayed in a bar chart view
2. **Details:** Information on events is displayed, but they are clustered and collapsed, so the UI is not overloaded
3. **List:** The events are displayed in a table view

In the above screenshot, the View Mode is **Counts**. Below is a screenshot of the **Details** View Mode.

![](https://i.imgur.com/PhduaN5.png)

The numbers (seen above) indicate the number of clustered/collapsed events for a specific time frame. For example, for /Windows, there are 130,257 events between 2009-06-10 and 2010-03-18. See the below image.

![](https://i.imgur.com/2BOolNk.png)

To expand the cluster, click on the `green icon with the plus sign`. See the below example.

![](https://i.imgur.com/F84vy7p.png)

To collapse the events, click on the `red icon with a minus sign`. Click `the map marker icon with a plus sign` if you wish to pin a group of events. This will move (pin) the events to an isolated section of the Events view.

![](https://i.imgur.com/CEMi881.png)

To unpin the events, click on the `map marker with the minus sign`. The last group of icons to cover are the `eye` icons. If you wish to hide a group of events from the Events view, click on the `eye with a minus sign`. In the below screenshot, the clustered events for /Boot were hidden and placed in the `Hidden Descriptions` (in the Filters area)

![](https://i.imgur.com/5Bed1O6.png)

If you wish to reverse that action and unhide the events, right-click and select `unhide and remove from list`. See the below example.

![](https://i.imgur.com/Sv7EDKe.png)

Last but not least, a screenshot of the **List** View Mode is below.

![](https://i.imgur.com/MXbQVVv.png)

This should be enough information to get you started interacting with the Timeline with some level of confidence.

