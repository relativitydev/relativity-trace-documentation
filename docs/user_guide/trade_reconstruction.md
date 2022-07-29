---
layout: default
title: Trade Reconstruction
parent: User Guide
nav_order: 10

---

# Trade Reconstruction
{: .no_toc }

Trade Reconstruction is used to automatically link trade and orders from Order Management Systems (OMS) or Trade Capture systems to their related communications.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Overview

There are several components to Trade Reconstruction. To begin, a Trade Reconstruction Configuration must be created. Trade Reconstruction Configurations are defined by administrators during implementation, more configuration information found [here]({{ site.baseurl }}{% link docs/administrator_guide/trade_reconstruction.md %}). Once a Trade Reconstruction Configuration is created, Trades can be reconstructed.

## Creating or Ingesting a Trade

To run Trade Reconstruction, you need a Trade. Trades can be created manually following the steps below or created through an integration with an OMS or Trade Capture system. Trade integrations are configured by administrators during implementation, more information can be found [here]({{ site.baseurl }}{% link docs/administrator_guide/trade_reconstruction.md %}).

**Manually Creating a Trade**

1. Navigate to the `Trades` tab and click `New Trade`.
2. Fill out the fields related to the Trade and click save

## Perform Trade Reconstruction

To run Trade Reconstruction, follow the steps below:

1. Navigate to your Trade on the `Trades` tab.
2. Click `Edit`
3. On the **Perform Reconstruction** field, select `Yes`
   - This will change the **Reconstruction Status** to `Pending`
   - This field selection will be changed back to `No`, allowing you to select `Yes` the next time you want to Reconstruct this Trade
4. Click `Save`

Your Trade will be fully Reconstructed when the **Reconstruction Status** field says `Complete`.

If you choose to perform Reconstruction again on Trade that has already been Reconstructed, this will completely remove any information about the previous Reconstruction.
{: .danger }

## Trade Reconstruction Fields

| **Field Name** | **Description**          | **Notes**    |
| ------------------------ | ----------------------------- | ----------------- |
| Identifier              | The name of the Trade.             |         |
| Reconstruction Status             | Shows the current status of the Trade during Trade Reconstruction. This field can be *empty* (Trade reconstruction has not been performed), `Pending` (Trade is waiting to begin Trade Reconstruction), `InProgress` (Trade is in the process of being Reconstructed), `Complete` (Trade has successfully finished being Reconstructed), `Errored` (Trade Reconstruction has failed to Reconstruct this Trade). |    This field is not editable.     |
| Last Reconstruction Time             | The date and time that the previous Reconstruction began.      |   This field is not editable.      |
| Last Reconstruction Completion Time  | The date and time that the previous Reconstruction completed.   | This field is not editable.  |
| Last Reconstruction Performed By User Artifact ID   | The Artifact ID of the User that performed the previous Reconstruction.      |   This field is not editable.      |
| Trade Reconstruction Action Count             | The number of times the Trade has been reconstructed.        | This field is not editable. This count is total number of times `Perform Reconstruction` is set to `Yes`, meaning it counts both completed and errored Reconstructions.   |
| Error Details   | If the Trade is in `Errored` status, this field displays why the Reconstruction may have failed.   | This field is not editable.  |
| Perform Reconstruction      | A Yes/No field that if set to `YES` will begin the Trade Reconstruction process.      |   See "Perform Trade Reconstruction section for more information.      |
| Reconstruction Configuration        | The configuration that will be used to perform the Trade Reconstruction action.        |  Admins will create and manage Reconstruction Configurations and define which should be used in each Trade Reconstruction case. Administrator information on how to set up a Trade Reconstruction Configuration can be found [here]({{ site.baseurl }}{% link docs/administrator_guide/trade_reconstruction.md %})     |


