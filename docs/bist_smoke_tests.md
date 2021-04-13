# Relativity Trace Automated Tests (BIST)

* [How to Run **BIST**](#how-to-runbist)
* [Manual Tests](#manual-tests)
  + [Pre-requisites](#pre-requisites)
  + [Test Verification **[AUTOMATED]**](#test-verification-automated)

Trace BIST (Built-in self test) contains automated tasks that perform basic smoke tests to ensure that
Relativity and Trace have been set up and configured properly. You only need to enable BIST, and let it 
run on its own.

Manual Tests are recommended but not required to be run. Steps marked with
**[AUTOMATED]** in the Manual Tests section are already part of Built-in self-test (**BIST**). If you decide
to run Manual Tests, it is recommended that you run **BIST** first.


## How to Run **BIST**

> **NOTE:** BIST must be run on a separate, dedicated non-production workspace. This is because **BIST** creates test documents/rules/terms that do not get removed.

-   First, you must set the Trace Configuration "Run Option" to Continuous
-   Navigate to -\> Trace -\> Setup
-   Click Edit, and set Run Option = Continuous

![](media/BIST_RunOptionContinuous.png)

-   Next, click "Built-in self-test (**BIST**)" link in the console

![](media/de731dd917844e3c4429763b8f7b6624.png)

-   If the "Built-in self-test (**BIST**)" link does not appear, follow these steps:
      - Navigate to Instance Settings
      - Under "Name", filter for TraceWorkspaceSettings, and edit this setting
      - Change WorkspaceID from 0 to the ArtifactID value of your BIST workspace
      - Change IsBISTEnabled from false to true
      - Click Save

![](media/BIST_TraceWorkspaceSettings.png)

-    Return to Setup tab in your BIST workspace
      - You should now be able to click on the "Built-in self-test (**BIST**)" link in the console
-   Click Edit on Built-In Self Test (BIST) Task Type, set Enabled to Yes and click Save

![image-20191218145522629](media/bist_smoke_tests/image-20191218145514143.png)

> **NOTE:** Once test completes Last Execution Status field will update to "Completed. Succeeded - Trace Test GoldenFlow Test." and the task will auto-disable itself.

![image-20191218145951065](media/bist_smoke_tests/image-20191218145951065.png)

## Manual Tests

### Pre-requisites

1.  Create a new Test Workspace

2.  Install the Trace application

    1.  Navigate to Library Application (Admin), locate Trace and install it
        into Test Workspace

    2.  Ensure that Trace Agent and all dependent Agents are enabled and working 

    3.  Within the workspace, navigate to Trace → Setup and set Run Option →
        Continuous

3.  Data Setup

    1.  Online Data Setup: Office 365 [Follow steps in [User Documentation](user_documentation.md#microsoft-exchange-data-source)]

        1.  Enable the data source

        2.  Ensure documents correctly processed throughout the pipeline

    2.  Offline Data Setup: Sample Data Source **[AUTOMATED]**

        1.  Create test data source (Trace BIST Data Source)

        2.  Create Data Transformations

            1.  Replace

            2.  Deduplication

        3.  Create and link Monitored Individuals

        4.  Generate test data emails with attachments

        5.  Extract and Ingest 148 documents with various file types, language
            contents across 2 data batches

4.  Create Terms **[AUTOMATED]**

    1.  problem\*

    2.  suffering

    3.  коррупц\*

    4.  protect against

    5.  "message is ready to be sent"
    
    6.  Lorem Ipsum
    
    7.  Test rule evaluation
   
    8.  "Nederlandsprekendes"  

5.  Create Document Folders **[AUTOMATED]**

    ![](media/ec3755ab72fd53aa637090fcf7d6787a.png)

6.  Create Saved Searches **[AUTOMATED]**

    ![](media/707823C7-1856-4831-9564-D06D105DDEA9.PNG)
    
7. Update Rule Evaluation task **[AUTOMATED]**
  
    ![](media/E1EE69E1-42DA-45FA-8E97-BD7407012B21.png)

8.  Create Rules **[AUTOMATED]**

    ![](media/408104f8f017cda4fa136c47acfe8038.png)

    1.  Create new Trace BIST - Basic Rule

        1.  Create a new rule (“Trace BIST - Basic Rule*”*) with “Trace BIST -
            Documents” saved search

        2.  Associate Terms created above

        3.  Associate Default Tag and Default Advanced actions

        4.  Enable rule

    2.  Create new Trace BIST - Data Retention Rule

        1.  Create a new rule (“Trace BIST - Data Retention Rule*”*) with “Trace
            BIST - Recycle Bin” saved search

        2.  Associate Trace BIST - Data Retention Action

        3.  Enable rule

    3.  Create new Trace BIST - Move To Folder Rule

        1.  Create a new rule (“Trace BIST - Move To Folder Rule*”*) with “Trace
            BIST - Documents” saved search

        2.  Associate Trace BIST - Move To Folder Action

        3.  Associate Terms: suffering

        4.  Enable rule
9. Create Rule Generator test object types **[AUTOMATED]**
  
    ![](media/bist_smoke_tests/BIST_RuleGeneratorObjectTypes.png)
    
10. Create Rule Generators **[AUTOMATED]**
  
    ![](media/bist_smoke_tests/BIST_RuleGenerators.png)
    
    
### Test Verification [AUTOMATED]

**Final expected state of the documents in workspace:**

- Trace BIST Data Source Generated Batches: `2`

- Total Documents in Trace BIST folder: `147`

- Total Deleted Documents: `1`

- Total Documents Matching Basic Rule: `6`

- Document Status: 
    - `3 - Term Searched` - 2
    - `5 - Ready for Rule Analysis` - 143
    - `6 - Alert Rules Complete` - 2
    
- Documents fields (Trace Hour Of The Day \| Trace Day Of Week): `populated` for all documents with `5 - Ready for Rule Analysis` and `6 - Alert Rules Complete` status

![](media/0AA3E43F-2873-4D49-BAB0-7E6566B9E50D.PNG)

- Number of rules generated by rule generators: `2`

- Number of documents matched with rule generated by `BIST Trade RG`: `143`

- Number of documents matched with rule generated by `BIST Watchlist RG`: `1`

**Additional Verification:**

1.  Trace custom audits are generated:

    ![](media/c0ba0573820c03995397d872facb2bb7.png)

2.  Data Batch Retry/Abandon mass-operations work (re-triggers import of data):

    ![](media/df8d7d265f3eb5ff3cc04bd60c5e4369.png)

3.  Trace Document Retry mass-operations work (re-submits documents through
    Trace flow, but does not re-trigger import):

![](media/c618f2acac67b761cec5c75a03932eec.png)
