Adminstration of Automation
=======================================================

.. include:: nav.rst

Users can create their own .BAT files to run jobs defined in the Automation Manager. Only SAS Adminstrators can create scheduled tasks on the SAS server. Users should coordinate with 
SAS Admin in CIS to create the SAS job under an appropriate service account on SGSASFSV1. |rule|

Admins will create .BAT files based on the specifications provided by the user, with some adjustments to allow the service account to execute the jobs while
not logged into the server. The .BAT files are located on \\SGSASFSV1\\automation\\[group].

**Example of a .BAT file for Scheduled Task on SGSASFSV1**
----------------------------------------------------------

    .. raw:: html    
        
        <div style="background-color:#ffffe6;width:100%;border-radius: 25px;padding: 20px; ">
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">@echo off</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">net use u: \\sgsasfsv1.corp.seagen.com\Pub</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">net use i: \\sgsasfsv1.corp.seagen.com\Infrastructure</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">net use o: \\sgsasfsv1.corp.seagen.com\Biometrics</i><br/ ><br/>
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">"E:\infrastructure\deploy\auto_gsdb\RunSAS.exe" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Auto" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Current"  ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Quiet" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"S:\Projects\GSDB\utilities\admin\auto_logs"</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"QC_Normal" </i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Auto"</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">Exit 0</i><br/ >
        </div>

