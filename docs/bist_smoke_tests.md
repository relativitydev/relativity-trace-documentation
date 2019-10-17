# Relativity Trace Automated Tests (BIST)

* [How to run **BIST**](#how-to-run---bist--)
* [Tests](#tests)
  + [Pre-requisites](#pre-requisites)
  + [Test Verification **[AUTOMATED]**](#test-verification----automated---)

This document describes steps needed to perform basic smoke tests to ensure that
Relativity and Trace have been set up and configured properly. Steps marked with
**[AUTOMATED]** are already part of Built-in self-test (**BIST**). Recommended
approach is to run **BIST** first and then perform remaining ad-hoc (manual)
tests after that. 

> **NOTE:** BIST must be ran on a separate, dedicated non-production workspace.

## How to run **BIST**

It is recommended to run **BIST** on a new workspace or on a test workspace as
**BIST** creates documents/rules/terms that do not get removed.

-   Navigate to -\> Trace -\> Setup and click Built-in self-test (**BIST**) link

![](media/de731dd917844e3c4429763b8f7b6624.png)

-   Click Edit on Sandbox Task Type, set Enabled to Yes and click Save

![](media/bff924ad11b5aea52e5ef3da32250f08.png)

> **NOTE:** Once test completes Last Execution Status field will update to "Completed. Details: Smoke Test Succeeded!" and task will auto-disable itself

![](media/3365ee39624ff425c6b6d0c74ddf92c9.png)

## Tests

### Pre-requisites

1.  Create a new Test Workspace

2.  Install Trace application

    1.  Navigate to Library Application (Admin), locate Trace and install it
        into Test Workspace

    2.  Ensure that Trace Agent and all dependent Agents are enabled and working 

    3.  Within the workspace, navigate to Trace → Setup and set Run Option →
        Continuous

3.  Data Setup

    1.  Online Data Setup: Office 365 [Follow steps in Documentation]

        1.  Enable data source

        2.  Ensure documents are pulled through

    2.  Offline Data Setup: Sample Data Source **[AUTOMATED]**

        1.  Create test data source (Trace BIST Data Source)

        2.  Create Data Transformations

            1.  Replace

            2.  Deduplication

        3.  Create and link Monitored Individuals

        4.  Generate test data emails with attachments

        5.  Extract and Ingest 144 documents with various file types, language
            contents across 2 data batches

4.  Create Terms **[AUTOMATED]**

    1.  problem\*

    2.  suffering

    3.  коррупц\*

    4.  protect against

    5.  "message is ready to be sent"

5.  Create Document Folders **[AUTOMATED]**

    ![](media/ec3755ab72fd53aa637090fcf7d6787a.png)

6.  Create Saved Searches **[AUTOMATED]**

    ![](media/6d0cd301b1ccf52ca71ced8b85e611b8.png)

7.  Create Rules **[AUTOMATED]**

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

### Test Verification **[AUTOMATED]**

**Final expected state of the documents in workspace:**

- Trace BIST Data Source Generated Batches: `2`

- Total Documents in Trace BIST folder: `143`

- Total Deleted Documents: `1`

- Total Documents Matching Basic Rule: `6`

- Document Status: `3 - Term Searched`

- Documents fields (Trace Hour Of The Day \| Trace Day Of Week): `populated`

![](media/a81e3661b864ceccb66f8842afdca832.png)

**Additional Verification:**

1.  Trace custom audits are generated:

    ![](media/c0ba0573820c03995397d872facb2bb7.png)

2.  Data Batch Retry/Abandon mass-operations work (re-triggers import of data):

    ![](media/df8d7d265f3eb5ff3cc04bd60c5e4369.png)

3.  Trace Document Retry mass-operations work (re-submits documents through
    Trace flow):

![](media/c618f2acac67b761cec5c75a03932eec.png)
