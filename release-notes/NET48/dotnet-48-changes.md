# .NET Framework 4.8 Release Notes

.NET Framework release notes describe product improvements grouped by product area. Each change includes a Microsoft-internal VSTS bug ID, the primary binary that was updated and whether the change was a bug or a feature.

## ASP.NET

* Fix handling of InputAttributes and LabelAttributes for ASP.NET CheckBox control. [643614, System.Web.dll, Bug, Build:3646]

## BCL

* Fixed deserialization of Collections which uses culture aware StringComparer. [566534, mscorlib.dll, Bug, Build:3621]
* Fixed System.Runtime.CompilerServices.RuntimeFeature.IsSupported to correctly account for application compatibility quirk settings for the Portable PDB feature introduced in .NET Framework 4.7.1. [571206, mscorlib.dll, Bug, Build:3621]
* Fixed the exception by parsing Japanese dates that have the year number exceeding the number of years in that date era. The behavior change will be noticed only if someone tries to parse a date containing some era and year while the year exceeds the last year in that era. [590659, mscorlib.dll, Bug, Build:3621]
* By default, elevated processes will not read HKCU for managed COM activation information. [592187, clr.dll, Bug, Build:3621]
* Fixed the serialization compatibility issue for CultureAwareComparer class. [621387, mscorlib.dll , Bug, Build:3632]
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

## ClickOnce

* Fixed Clickonce UI dialogs on high Dpi machines with scale set to more than 100% for both new and existing applications which scale upto 300%. In the scenario where user wants to see legacy images, there is an opt out switch "Switch.System.Windows.Forms.UseLegacyImages" that can be set to "true" in dfsvc.exe.config file. [389534, Microsoft.Build.Tasks.v4.0.dll, Bug, Build:3621]
* Fixed Mage so it can properly update the identity of dependent assemblies in ClickOnce application manifests. [534286, Microsoft.Build.Tasks.v4.0.dll, Bug, Build:3621]
* Fixed ClickOnce dialogs (Splash screen, Install progress dialog, Maintenance dialog and Update dialog) have accessibility issues as mentioned in this bug. Fix is for realigning control indices and setting accessible names where it was missing. [541886, Microsoft.Build.Tasks.v4.0.dll, Bug, Build:3621]
* Fixed progress bar alignment from Right to Left in Splash Screen and Download progress dialog for ARA & HEB languages for ClickOnce UI. Fixed RTL layout in the ClickOnce dialogs. Individual controls are to be set in RTL layout as this property is not propagated. Set this property explicitly on progress bar control. [552893, Microsoft.Build.Tasks.v4.0.dll, Bug, Build:3621]

## CLR

* Fixed LoadFrom(String, Byte[], AssemblyHashAlgorithm) works with SHA2 algorithms. [229901, mscorlib.dll, Bug, Build:3621]
* Reduced AsyncLocal memory overhead on value change. [470761, mscorlib.dll, Bug, Build:3621]
* Improved spin-waits in several synchronization primitives to perform better on Intel Skylake and more recent microarchitectures. [495945, mscorlib.dll, Bug, Build:3621]
* Fixed issues where incorrect values are sent to EventListeners. This includes incorrect activity ids on start and stop events and improper EventLevel values. [581072, mscorlib.dll, Bug, Build:3621]
* Fixed a potential crash with concurrent calls to a new dynamic method. [581154, mscorlib.dll, Bug, Build:3621]
* Fixed a possible deadlock when calling Dispose() on an EventSource. [597221, System.Core.dll, Bug, Build:3621]
* The ‘shadowCopyVerifyByTimestamp’ setting is now configurable for individual appdomains, as opposed to being a process wide setting. This helps in situations where you may not be the host process, but want to configure a new appdomain that verifys timestamps when shadow copying. [565570, clr.dll, Bug, Build:3632]
* Addressed the issue where the JIT compiler optimized away a call to the CompareExchange intrinsic operation under specific conditions [638227, clrjit.dll, Bug, Build:3646]

## Networking

* Fixed a memory leak issue in HttpWebRequest when communicating with a HTTPS server through a proxy. [484621, System.dll, Bug, Build:3621]
* Fixed HTTP Status line parsing to be more tolerant of missing status description text in HTTP responses. [534936, System.dll, Bug, Build:3621]
* Fixed a NetworkInformation.NetworkChange deadlock scenario when there is a lock around NetworkChanged listener and user’s callback. [554780, System.Net.NetworkInformation.dll, System.dll, netstandard.dll, Bug, Build:3621]

## SQL

* Fixed the issue that SqlDataReader.ReadAsync() runs synchronously. Now the method runs asynchronously as expected. [594433, System.Data.dll, Bug, Build:3621]
* Fixed the issue while using SqlConnection.ConnectionString to set a null or empty connection string, an NRE exception will be thrown by the usage of the API in .Net Framework 4.7.2. [613944, System.Data.dll, Bug, Build:3621]
* Fixed the following issue relevant to SQL: while connecting to Azure SQL DB using .NET 4.7.2, using MultipleActiveResultSets=true in the connection string with System.Data.SqlClient.SqlConnection, async query operations sometimes lead to a bad TDS protocol request stream to be sent from the client, causing the Async Query APIs to fail connection string. [624283, System.Data.dll, Bug, Build:3632]
* Fixed a bug where SqlClient login may use an infinite timeout due to truncating a small millisecond timeout to zero when converting to seconds. [647908, System.Data.dll, Bug, Build:3646]

## WCF

* Fixed an accessibility problem in WCF Trace Viewer that caused ComboBox controls to be themed incorrectly in High Contrast themes. [424922, SvcTraceViewer.exe, Bug, Build:3621]
* Fixed the race-condition that exists in AsyncResult that closes a WaitHandle before Set() is called. When this happens, the process crashes with an ObjectDisposedException. [552736, System.ServiceModel.Internals.dll, Bug, Build:3621]
* Fixed race-condition when aborting connections which caused ObjectDisposedException to be thrown in CleanupChannelCollections. [586151, mscorlib.dll, Bug, Build:3621]
* Fixed a high lock contention issue when a large number of threads calling WCF serialization logic [570201, System.Runtime.Serialization.dll, Bug, Build:3646]

## Windows Forms

* Enabled labels are now always rendered using a high contrast text color when a high contrast mode is enabled. This change is effective in applications that are recompiled to target .NET Framework 4.8. [486578, System.Windows.Forms.dll, Bug, Build:3621]
* Maximize/Minimize button of new child Form are not scaled well on HDPI  devices because of image property set to not to scale. On 100% dpi machines scaling it not required but on high dpi devices, when scaling set to more than 100%, the images set for Maximize/Minimize boxes need to be scaled. [515092, System.Windows.Forms.dll, Bug, Build:3621]
* Checkbox height is changed from square to rectangle when scaled. Padding and margins were scaled, thus adding to already scaled height of the checkbox as we were using item height to draw checkbox instead of checkbox height. Earlier these margins/paddings were constants and ignorable pixel sizes, and were not visible. [528418, System.Windows.Forms.dll, Bug, Build:3621]
* The new UIA behavior for CheckedListBox control has been introduced: the first checkbox item in the CheckedListBox control is now announced by Narrator when focus moves to the control without any selected item. This change is effective in applications that were recompiled to target .NET Framework 4.8. [533226, System.Windows.Forms.dll, Bug, Build:3621]
* The new behavior for disabled link labels has been introduced: link labels' enable/disable state is now provided correctly - disabled links have IsEnabled = false Accessibility Property and read by Narrator as 'Some Link, disabled'. This change is effective in applications that were recompiled to target .NET Framework 4.8. [537224, System.Windows.Forms.dll, Bug, Build:3621]
* The new behavior for link label with defined link area has been introduced: link area accessible name is now read by Narrator as full text of the parent link label. This change is effective in applications that were recompiled to target .NET Framework 4.8. [537934, System.Windows.Forms.dll, Bug, Build:3621]
* Improved accessibility for the DateTimePicker control. In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. [543580, System.Windows.Forms.dll, Bug, Build:3621]
* An associated label name is now used as an accessible name for DateTimePicker control when AccessibleName property is not set. The default DateTimePicker's AccessibleRole is ComboBox now. These changes are effective in applications that were recompiled to target .Net Framework 4.8. [544791, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed issues to add support for UIA live regions to WinForms. Added support for notifications about the Text property changes to the Label class (through UIA Live Regions). [545374, System.Windows.Forms.dll, Bug, Build:3621]
* Application Files' and 'Application Directory' label text is truncated on localized OSes. Developers will not be able to see the shortcut information for this control on the UI. This fix helps to resolve that issue and always show the full text of the label . [549024, System.Windows.Forms.dll, Bug, Build:3621]
* The new UIA behavior for numeric and domain up-down controls has been introduced: numeric and domain up-down controls without labels (custom UIA name) are announced by Narrator as 'spinners'. This change is effective in applications that were recompiled to target .NET Framework 4.8. [549543, System.Windows.Forms.dll, Bug, Build:3621]
* The new UIA behavior for CheckedListBox control has been introduced: an empty CheckedListBox control now has a focus rectangle drawn for a virtual first item when the control becomes focused. This change is effective in applications that were recompiled to target .NET Framework 4.8. [549558, System.Windows.Forms.dll, Bug, Build:3621]
* Improved ListView accessibility by enabling showing grey rectangle around the selected ListView item when parent ListView is out if focus. This change is effective in applications that were recompiled to target .NET Framework 4.8. [564762, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed VisualStyle property in Winforms, is checking for supported values (by Winforms) and any value that goes outside of this range, Winforms throws an exception. Winforms also checks if the VisualStyle property set is supported by Winforms when it is using this property and does no-op if it is not supported. Underlying native method we use to set visual styles does not care what the value for visualstyle is being passed to it. Making this change will align Winforms code with windows and does not throw exception but still validate supported visual styles when using this property. Removing the validation condition while setting this property. [578093, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed the DataGridView's Combobox expand/collapse state accessible for the customers who use assistive technologies. In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>    
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/>. [574309, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed and improved the stability of Live Regions feature by adding LiveSetting property setter check. This feature is available starting with Windows 10, version 1709 (RS3).
In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/>. [583863, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed Winforms application and controls, when enable for ""per-Monitor"" Dpi aware, they are not scaled according to the dpi of the monitor ( or device). Winforms app by default behave like ""System"" Dpi aware. This is causing Winforms applications/controls to be displayed ""blur"" as a result of windows scaling them and in some cases, controls are either not scaled or scaled out of proportionate. Made changes on control level to respond to DPI change event (assuming  windows raise this event whenever there is a DPI change) and rescale controls according to the new DPI. [597091, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed by adding support for UIA notification event to Label and GroupBox classes. This feature is available starting with Windows 10, version 1709 (RS3). In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/>. [563596, Windows.UI.Xaml.Automation.Peers.dll, Windows.dll, Bug, Build:3621]
* Fixed by adding support for the live region feature to the ToolStripStatusLabel class. In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/>. [564300,Windows.UI.Xaml.Automation.Peers.dll, Windows.dll, Bug, Build:3621]
* Fixed by improving the accessibility of DataGridView and ListView to make sort direction available via UIA: added exposing sort order and sort column via ItemStatus property and column name. This change is effective in applications that were recompiled to target .NET Framework 4.8. [549288, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed by making the forward and backward toolstrip navigation consistent. This feature is available starting with Windows 10, version 1709 (RS3). In order for the application to benefit from these changes, the application should be recompiled to target .NET Framework 4.8 or the application should explicitly opt-in into all accessibility app context switches in the app.config file. For example:
    <?xml version=""1.0"" encoding=""utf-8""?>
    <configuration>
    <runtime>
        <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
        <!-- Enabling newer accessibility features (e.g. UseLegacyAccessibilityFeatures.2=false) requires all older accessibility features to be enabled (e.g. UseLegacyAccessibilityFeatures=false) -->
        <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false""/>
    </runtime>
    </configuration>
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches:
<AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/>. [544592, System.Windows.Forms.dll, Bug, Build:3621]
* Fixed the announcement of DataGridView Read-only TextBox cells by making accessible and clear: editable TextBoxes are announced as 'editable' and read-only TextBoxes are announced as 'read-only'. This change is effective in applications that were recompiled to target .NET Framework 4.8. [599936, System.Windows.Forms.dll, Bug, Build:3621]
* Added support for UIA notification event to ProgressBar class. The feature is available starting with Windows 10, version 1709 (RS3). [581351, System.Windows.Forms.dll, Bug, Build:3632]
* Fixed an issue where read-only Status for DataGridView TextBox column is not announced by Narrator. This change is effective in applications that were recompiled to target .NET framework 4.8. [599936, System.Windows.Forms.dll, Bug, Build:3632]
* Fixed reliability issues in Graphics class when used in RDP sessions. [627739, System.Drawing.dll, Bug, Build:3632]
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
In order for an application that targets .NET Framework 4.8 to opt out from this change, use the following combination of switches: <AppContextSwitchOverrides value=""Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=true""/>. [642548, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed RadioButton/ChecKBox controls truncation issue when control property is set to 'Flat/Popup style ' [645041, System.Windows.Forms.dll, Bug, Build:3646]
* Fixed Button control to scale according to monitor Dpi on which the control is being displayed. [656271, System.Windows.Forms.dll, Bug, Build:3646]
* Improved loading/rendering time for windows forms controls.  [662839, System.Windows.Forms.dll, Bug, Build:3646]

## WPF

* Fixed a memory leak arising when removing data items from their parent collections, when UIAutomation is present. [172291, PresentationFramework.dll, Bug, Build:3621]
* Fixed virtualizing ItemsControl hung during scrolling when Items collection contains duplicate value-typed objects. [360053, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF application can crash with NullReferenceException when changing a property used by a DataTrigger whose host element has been removed from the visual tree. The crash only occurs if the host element is garbage-collected during a small window of time during the property-change notification. [401484, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF app that has multiple top-level windows in different threads that crashes during a theme change. [404464, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF applications running on touch or stylus-enabled machines can sometimes hang at startup or during connection of a tablet or stylus device. [474688, PresentationFramework.dll, Bug, Build:3621]
* Fixed focus issues in WPF applications running in high contrast themes, it can be difficult to distinguish when a TextBox, PasswordBox, or RichTextBox has focus. [486957, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF applications using DocumentViewer controls may see issues with the rendering of text selection graphics after a theme change. This change addresses that issue. [494408, PresentationFramework.dll, Bug, Build:3621]
* In WPF applications running on touch or stylus-enabled machines that set the AppContext switch "Switch.System.Windows.Input.Stylus.EnablePointerSupport" to true, StylusPlugins would not be properly unhooked when element properties were changed prior to the presentation source being set to null. This change fixes this issue. [500125, PresentationFramework.dll, Bug, Build:3621]
* Fixed an issue that caused XAML Browser Applications (XBAP’s) targeting .NET 3.5 to sometimes load using .NET 4.x runtime incorrectly. [560029, PresentationHost_v0400.dll, Bug, Build:3621]
* Fixed an infinite loop arising during layout of a Grid in some cases when *-columns with MinSize constraints consume all the available space. [560609, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF applications running under high contrast themes, the border color of a disabled TextBox, RichTextBox, and PasswordBox was incorrect. This change addresses that issue. [527669, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF applications using non-adorner based text selection for TextBox and PasswordBox (Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering=false), developers may now set the SelectionTextBrush property in order to alter the rendering of the selected text. By default, this color changes with SystemColors.HighlightTextBrushKey. If non-adorner based text selection is not enabled, this property does nothing. [531137, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF application running in high contrast mode has difficult to see selection visuals on DataGridCells. This change addresses that issue. [545871, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF applications running on a touch or stylus-enabled machine, users might periodically see a crash in System.Windows.Window.GetWindowMinMax. This change addresses that issue. [546769, PresentationFramework.dll, Bug, Build:3621]
* Fixed a memory leak arising when sending bitmaps to the clipboard. [589759, PresentationCore.dll, Bug, Build:3621]
* Fixed WPF application running on a stylus or touch-enabled machine may see NullReferenceExceptions or InvalidCastExceptions under certain circumstances. This change addresses this issue. [577690, PresentationCore.dll, Bug, Build:3621]
* Fixed issue when non-Adorner-based text selection is enabled in .NET Framework 4.7.2 and above, the default SelectionOpacity of FlowDocumentReader, FlowDocumentScrollViewer, and SinglePageViewer will cause the selection to obscure the underlying text. This change addresses this issue by setting the default SelectionOpacity to the correct value. [568305, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF applications using non-adorner based text selection (AppContext flag "Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering=false"), editable ComboBoxes do not appropriately follow theme colors for text selection. [572332, PresentationFramework.dll, Bug, Build:3621]
* Fixed timing issues in the finalizer thread could potentially cause exceptions during AppDomain or process shutdown in certain .NET applications. This is generally seen in applications that do not correctly shut down Dispatchers running on worker threads prior to process or AppDomain shutdown. Such applications should take care to properly manage the lifetime of Dispatchers. This change adds an AppContext switch that can help alleviate (but not eliminate) some of the issues that may arise from these application design issues. To enable this, set the AppContext flag "Switch.MS.Internal.DoNotInvokeInWeakEventTableShutdownListener=true". [606492, WindowsBase.dll, Bug, Build:3621]
* Fixed crash issues and allows the replace to proceed.When replacing multiple characters with a single character (in a different language than replaced text) using IMEPad, WPF crashes. [595046, PresentationFramework.dll, Bug, Build:3621]
* Fixed WPF application that changes TreeView.IsEnabled and (at the same time) changes the underyling collection(s) can experience a spurious ElementNotAvailableException. [573999, PresentationFramework.dll, Bug, Build:3621]
* Addressed the issue of high CPU usage or hangs. This used to happen under certain conditions, where, WPF applications using WindowChromeWorker experience high CPU usage or hangs. . [437642, PresentationFramework.dll, Bug, Build:3632]
* Fixed a bug in the 4.7 algorithm for allocating sizes to *-rows in a Grid. In some cases (e.g. Grid with Height="Auto" containing empty rows), rows were arranged at the wrong position, possibly outside the Grid altogether. [590061, PresentationFramework.dll, Bug, Build:3632]
* Fixed a potential deadlock in WPF Packaging APIs when multiple threads were both creating and closing large packages simultaneously. [609850, PresentationCore.dll, WindowsBase.dll, Bug, Build:3632]
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

## WorkFlow

* We have modified the hashing algorithm used to generate XOML file checksums when building projects with XOML files. If this causes problems, the previous hashing algorithm can be used by specifying ""true"" for the following AppContext switch: Switch.System.Workflow.ComponentModel.UseLegacyHashForXomlFileChecksum. Note that this AppContext switch applies to the MSBuild process, so must be specified in the ""config path"" of the MSBuild.Exe that is used to perform the builds. [531054, System.Workflow.Runtime.dll, Bug, Build:3621]
* We have modified the hashing algorithm used to calculate keys to internal in-memory caches. If this causes problems, the previous hashing algorithm can be used by specifying ""true"" for the following AppContext switches: Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey. [532505, System.Workflow.Runtime.dll, Bug, Build:3621]"
* Fixed default hashing algorithm that help debugging symbols has changed. If you encounter problems with breakpoints in the workflow designer not being hit when expected, you may have a mismatch of hashing algorithms between MSBuild and the project being debugged. The following AppContext switch can be specified for MSBuild.exe and the project being debugged to help alleviate the problem. Switch.System.Activities.UseLegacyHashForDebuggerSymbols If this switch has a value of ""true"", then the default hashing algorithm for pre-4.7.2 versions of .NET are used. If the value of the switch is ""false"", the newer default hashing algorithm is used. [537692, System.Workflow.Runtime.dll, Bug, Build:3621]
* Previously, under extreme usage conditions (high volume of connections to MSDTC), it was possible for a CriticalSection to be held by a single thread indefinitely, resulting in the need to restart the process. This problem has been resolved. In addition, some object caches that would help performance in multi-threaded scenarios were not taken advantage of correctly. This has been resolved. [540812, System.Workflow.Runtime.dll, Bug, Build:3621]
* Fixed an accessibility problem to enable connector label reading on workflow designer [604810, System.Activities.Presentation.dll, Bug, Build:3646]
* Fixed an accessibility problem to have more texts clearly visible on workflow designer. [613975, System.Activities.Presentation.dll, Bug, Build:3646]
* Fixed the StackOverflowException issue for larger nesting depth of XOML. Previosuly, if the object nesting depth in the XOML was large, there were possibilities to cause the process to encounter a StackOverflowException. These problems have been resolved. 
The maximum object nesting depth can be adjusted (default being 300) with the following AppSetting specification in the process that creates and invokes the WorkflowCompiler class:
<add key=""""microsoft:WorkflowComponentModel:XOMLMaximumNestedObjectDepth"""" value=""""n""""/>
Where n is the new maximum object nesting depth.
The possible issues like, random code execution during XOML deserialization (even when CheckTypes parameter is specified to the WorkflowCompiler), have been resolved [631082, System.Workflow.ComponentModel.dll, Bug, Build:3646]
