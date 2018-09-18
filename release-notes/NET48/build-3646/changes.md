# .NET Framework Build 3646 Release Notes
Following changes are included in .NET Framework 4.8 build 3646. You can view the full list of [.NET Framework 4.8 Changes](/release-notes/NET48/dotnet-48-changes.md) (all changes, including those in build 3646 and builds upto current date).

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## ASP.NET

* Fix handling of InputAttributes and LabelAttributes for ASP.NET CheckBox control. [643614, System.Web.dll, Bug, Build:3646]

## BCL

* Upgraded the System.IO.Compression zlib (inside clrcompression.dll) to the latest zlib version 1.2.11 [532490, clrcompression.dll, Bug, Build:3646]
* Fixed by reducing memory  allocations in hashing with the CAPI classes (SHA256CryptoServiceProvider, et al) [548940, System.Core.dll, Bug, Build:3646]
* Fixed by reducing memory allocations in hashing with the CNG classes (SHA256Cng, et al) [548941, System.Core.dll, Bug, Build:3646]
* Fixed the issue of System.DateTime returning the wrong time after Windows processes a leap second, by following changes:
DateTime and DateTimeOffset will work with the leaps seconds reported by Windows RS5 systems. DateTime.Now and DateTime.UtcNow will always be synchronized with the system time. 
DateTime and DateTimeOffset will never report the leap second as value 60, instead, it’ll always report it as 59. 
DateTime and DateTimeOffset operations will continue to work as it used to work, i.e. internally always handle the minutes as 60 seconds which make it compatible with the down levels platforms. [641206, mscorlib.dll, clr.dll, Bug, Build:3646]
* Fixed WCF de-serialization failure issue of CultureAwareComparer object. Fixed the issue where Applications using WCF to communicate with web services or applications using data contract serialization directly, were experiencing failures to deserialize the CultureAwareComparer object. [645084, mscorlib.dll, Bug, Build:3646]
* Reduced the impact of the "FIPS mode" bit being set in the OS [653796, mscorlib.dll;System.Core.dll, Bug, Build:3646]
* Changed default content encryption algorithm of EnvelopedCms to AES. [656518, System.Security.dll, Bug, Build:3646]

## CLR

* Addressed the issue where the JIT compiler optimized away a call to the CompareExchange intrinsic operation under specific conditions [638227, clrjit.dll, Bug, Build:3646]

## SQL

* Fixed a bug where SqlClient login may use an infinite timeout due to truncating a small millisecond timeout to zero when converting to seconds. [647908, System.Data.dll, Bug, Build:3646]

## WCF

* Fixed a high lock contention issue when a large number of threads calling WCF serialization logic [570201, System.Runtime.Serialization.dll, Bug, Build:3646]

## Windows Forms

* Fixed accessible hierarchy of WinForms DataGridView control to represent its currently editing control (inner cell TextBox or ComboBox) as a child of corresponding editing cell. Added support of UIA notifications to DataGridView control. [442899, System.Windows.Forms.Dll, Bug, Build:3646]
* Fixed the issue of Narrator not announcing the updated value of ComboBox in PropertyGrid. 
Added support for UIA notification event to PropertyGrid. The feature is available starting with Windows 10, version 1709 (RS3). Added screen reader announcement for PropertyGrid's ComboBox value changes. Added ComboBox's text field update in response of ComboBox selection changes.
In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. App.config file content is shown below (in 642548). [508369, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed improper scaling of auto-sized controls when form is moved to secondary monitor with different DPI scaling. [515971, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed improper scaling of the System-style control's font on a Font-scaled form,  when Form is moved to a secondary monitor with different DPI scaling [519500, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed Checkbox and RadioButton control truncation issues control property is set to "FlatStyle". [519530, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed the improper scaling issue of auto-sized controls when form is moved to secondary monitor with different DPI scaling. All Controls (e.g. buttons) in the FlowLayout are placed into the first column with setting the AutoScroll property as True when DPI changed [525684, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed the WinForms control tooltip's issue where it does not appear when moving keyboard focus to the control
A control's tooltip is displayed now when a user uses a keyboard to focus the control.
This change is effective in applications that have Switch.System.Windows.Forms.UseLegacyToolTipDisplay value and either Switch.UseLegacyAccessibilityFeatures.3 value is set to false or application is built to target .NET version 4.8.  App.config file content is shown below (in 642548). [548792, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed font scaling issue when DPI changes. Winforms application and controls, when enabled for """"per-Monitor"""" Dpi aware, they are not scaled according to the dpi of the monitor (or device). Winforms app by default behave like """"System"""" Dpi aware.  This was causing Winforms applications/controls to be displayed """"blur"""" as a result of windows scaling them and in some cases, controls are either not scaled or scaled out of proportionate.
Made changes on control level to respond to DPI change event (assuming  windows raise this event whenever there is a DPI change) and rescale controls according to the new DPI [597091, System.Windows.Forms.dll, Bug, Build:3646]
* Added support of Accessibility Invoke pattern to DataGridView Image cell with ability to invoke cell's default action. (in case Image cell is actually an image of a button)
In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. App.config file content is shown below (in 642548). [615721, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed PropertyGrid control scaling issue in Winforms, when parent window DPI changed. PropertyGrid control in the .NET 4.8 runtime will now properly scale according to current running monitor DPI setting. Developer has to opt-in to this fix by either targeting to .NET 4.8 framework or using the .NET 4.8 opt-in config switch. [616661, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed Checkbox and RadioButton controls when set to 'FlatStyle' not being scaled on high Dpi monitors. [638326, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed DataGridView ComboBox accessible hierarchy. Introduced the support of ComboBox UIA notifications. The feature is available starting with Windows 10, version 1709 (RS3).
In order for the application to benefit from these changes, the application should be recompiled to target .NET framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. 
App.config file content: 
      <configuration>
        <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
       <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
       </runtime>
      </configuration>
In order for an application that targets 4.7.3 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/> 
[642548, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed RadioButton/ChecKBox controls truncation issue when control property is set to 'Flat/Popup style ' [645041, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed Button control to scale according to monitor Dpi on which the control is being displayed. [656271, System.Windows.Forms.dll, Bug, Build:3646]
* Improved loading/rendering time for windows forms controls.  [662839, System.Windows.Forms.dll, Bug, Build:3646]

## Workflow

* Fixed an accessibility problem to enable connector label reading on workflow designer [604810, System.Activities.Presentation.dll, Bug, Build:3646]
* Fixed an accessibility problem to have more texts clearly visible on workflow designer. [613975, System.Activities.Presentation.dll, Bug, Build:3646]
* Fixed the StackOverflowException issue for larger nesting depth of XOML. Previosuly, if the object nesting depth in the XOML was large, there were possibilities to cause the process to encounter a StackOverflowException. These problems have been resolved. 
The maximum object nesting depth can be adjusted (default being 300) with the following AppSetting specification in the process that creates and invokes the WorkflowCompiler class:
<add key=""""microsoft:WorkflowComponentModel:XOMLMaximumNestedObjectDepth"""" value=""""n""""/>
Where n is the new maximum object nesting depth.
The possible issues like, random code execution during XOML deserialization (even when CheckTypes parameter is specified to the WorkflowCompiler), have been resolved [631082, System.Workflow.ComponentModel.dll, Bug, Build:3646]

## WPF

* Fixed incorrect result of pressing an arrow key when focus is on a Hyperlink within an item that is not the SelectedItem of the parent ItemsControl. [405208, PresentationFramework.dll, Bug, Build:3646]
* Fixed issue where internal class PriorityQueue<T> can return items in the wrong order. [442569, PresentationCore.dll, Bug, Build:3646]
* Fixed usage of resources internal to theme files to avoid potential conflicts. [494194, System.Windows.Controls.Ribbon.dll, Bug, Build:3646]
* Fixed an issue where automation properties set on an editable RibbonComboBox are not properly announced by screen readers or other assistive technologies. [520147, PresentationCore.dll, Bug, Build:3646]
* GridViews with focusable Header rows will now not experience keyboard focus landing on the padding column in the header. [559546, PresentationFramework.dll, Bug, Build:3646]
* Fixed Binding's incorrect use of IList indexer when the source object declares a custom indexer with the same signature  [585942, PresentationFramework.dll, Bug, Build:3646]
* Fixed the issues of certain bounding rectangles, not being drawn corrently. When WPF is run in Per-Monitor Aware mode, certain bounding rectangles around text are drawn incorrectly by Accessibility tools like Narrator. This fix addresses the problem. To opt-into this fix, the target framework version of the Application should be set to .NET 4.8. Alternatively, an AppContext switch - "Switch.UseLegacyAccessibilityFeatures.2" - can be overridden with the value "false" to enable the fix.  [617457, PresentationFramework.dll, Bug, Build:3646]
* Fixed a hang arising during layout of a Grid when UseLayoutRounding=true, high DPI is in effect, grid *-column widths are determined from children with ColumnSpan > 1, and floating-point roundoff is unfavorable. [619978, PresentationFramework.dll, Bug, Build:3646]
* Fixed an issue where re-entrant calls during shutdown could cause various application faults in WPF applications running on a touch or stylus enabled machine. [633620, PresentationCore.dll, PresentationFramework.dll, Bug, Build:3646]
* Fixed a memory leak arising when the number of TextBoxes drops to 0. [645497, PresentationFramework.dll, Bug, Build:3646]
* Fixed the DeadLock issue faced during creation of Spellchecker while Finalizer is ending another Instance. Under certain circumstances, WPF applications using the spell-checker that use custom dictionaries could throw unexpected excpetions and crash [646599, PresentationFramework.dll, Bug, Build:3646]
* Addressed the issue where GroupItem headers containing an Expander were not announced correctly by screen readers [646633, PresentationFramework.dll, Bug, Build:3646]
* Fixed WPF issue of not creating correctly-size rendertarget for mixed-mode child windows. Under certain circumstances, per-monitor DPI aware applications that host WPF based controls or plugins were not rendering the WPF window fully [646801, wpfgfx_v0400.dll, Bug, Build:3646]
* Addressed the restore issue of Window.Left & Window.Top. When WPF applications are running in per-monitor aware mode, saving the value of Window.Left and Window.Top at application end, and restoring the values to a Window prior to creation upon the next application launch, was not restoring the application to the same screen position where it was at the time the application was closed. [646803, PresentationFramework.dll;PresentationCore.dll;WindowsBase.dll, Bug, Build:3646]
* Fixed the issue where HwndHost does not adapt child-HWND sizing correctly during DPI changes. When WPF is run in Per-Monitor Aware mode, controls hosted within HwndHost were not sized correctly after DPI changes (for e.g., when moving applications from one monitor to another). This fix ensures that controls hosted so are sized appropriately [646805, PresentationFramework.dll;PresentationCore.dll;WindowsBase.dll, Bug, Build:3646]
