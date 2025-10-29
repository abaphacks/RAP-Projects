# RAP-Projects
RAP Excel Upload/Download App Version 1

App Summary
The RAP (RESTful ABAP Programming) Excel Upload and Download App enables users to manage and upload development data through Excel files.
Key functionalities include:
- Upload Excel files containing development data and populate corresponding CDS child entities.
- Download a prefilled Excel template for data entry.
- Auto-update file and template statuses (e.g., File Selected, Uploaded, Present, Absent).
- Enable/disable front-end actions based on attachment and status values.
- Integration with Fiori/UI5 via OData service exposure.List of objects created  

Functional Flow

Upload Flow:
1. User selects an Excel file attachment.
2. The determination `FillSelectedStatus` updates file status.
3. `uploadExcelData` action reads and validates Excel content using XCO APIs.
4. Deletes existing child entries for the Employee/Development ID combination.
5. Creates new child records and sets `FileStatus = 'Excel Uploaded'`.

Download Flow:
1. User triggers `DownloadExcel` action.
2. The system generates an Excel template dynamically using XCO APIs.
3. Populates headers and updates Attachment field.
4. Sets `TemplateStatus = 'Present'` to mark template availability.

Main Components Created:
1. CDS Tables
   - `ZT2123_USER` (Parent) — Stores employee development data and attachment metadata.
   - `ZT2123_USER_DEV` (Child) — Stores parsed Excel rows (development objects).

2. CDS Views
   - `ZI_2123_USER`, `ZI_2123_USER_DEV` (Interface Views)
   - `ZC_2123_USER`, `ZC_2123_USER_DEV` (Projection Views)
3. Metadata Extensions
   - ZME_2123_USER
   - ZME_2123_USER_DEV
     
4. Service Definition
   - `ZSD_2123_USER_DEV_DETAILS` — Exposes projections for front-end consumption.

5. Behavior Definitions
   - Core and Projection Behaviors implementing upload/download actions, determinations, and side effects.

6. Behavior Handler Classes
   - `ZBP_I_2123_USER` — Global class containing types and constants.
   - `LHC_USER` — Local handler implementing methods like `uploadExcelData`, `DownloadExcel`, and determinations.

