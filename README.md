# WorkflowPOC
Proof of concept for Workflow designer issue with SDK based class libraries. This is a trimmed down version of issues i'm having in code at workplace.

This repo includes two projects
* ClassLibrary1 - Project with old format project system
* ClassLibrary2 - Project with SDK-based project system

Both projects contain Workflow Activities.

For Lib1, We can added arguments of types from current assembly. In this example, I have added Class1 as the in Argument.
![alt text](/Images/Lib1_Add_Arguments.png)
Exceprt from XAML:
  ```sh
  <x:Members>
    <x:Property Name="argument1" Type="InArgument(local:Class1)" />
  </x:Members>
```

This works without issues.

For Lib2, When adding new parameter, the types from current assembly are not visible. Only types from mscorlib are shown.
![alt text](/Images/Lib2_Add_Arguments.png)

Created another activity2, and added the above manually in XAML.

This results in Workflow designer exceptions.

*Exception 1*

```sh
Recoverable
System.NullReferenceException: Object reference not set to an instance of an object.

Server stack trace: 
   at Microsoft.VisualStudio.Activities.AddIn.WorkflowDesignerAddIn.OnReferenceUpdated(AssemblyName updatedReference, Boolean isAdded)
   at Microsoft.VisualStudio.Activities.AddInAdapter.IDesignerContractToViewAddInAdapter.OnReferenceUpdated(AssemblyName updatedReference, Boolean isAdded)
   at System.Runtime.Remoting.Messaging.StackBuilderSink._PrivateProcessMessage(IntPtr md, Object[] args, Object server, Object[]& outArgs)
   at System.Runtime.Remoting.Messaging.StackBuilderSink.SyncProcessMessage(IMessage msg)

Exception rethrown at [0]: 
   at System.Runtime.Remoting.Proxies.RealProxy.HandleReturnMessage(IMessage reqMsg, IMessage retMsg)
   at System.Runtime.Remoting.Proxies.RealProxy.PrivateInvoke(MessageData& msgData, Int32 type)
   at Microsoft.VisualStudio.Activities.DesignerContract.IDesignerContract.OnReferenceUpdated(AssemblyName updatedReference, Boolean isAdded)
   at Microsoft.VisualStudio.Activities.HostAdapter.IDesignerViewToContractHostAdapter.OnReferenceUpdated(AssemblyName updatedReference, Boolean isAdded)
   at Microsoft.VisualStudio.Activities.EditorPane.ReferencesEvents_ReferenceAdded(Reference reference)
   at Microsoft.VisualStudio.ProjectSystem.VS.Implementation.Package.Automation.OAVSReferences.<>c__DisplayClass34_0.<OnReferenceAdded>b__0()
   at Microsoft.VisualStudio.ProjectSystem.VS.HResult.<>c__DisplayClass37_0.<Invoke>b__0()
   at Microsoft.VisualStudio.ProjectSystem.VS.HResult.Invoke(Func`1 action, IServiceProvider vsShellServiceProvider, IProjectFaultHandlerService projectFaultHandlerService, UnconfiguredProject project)
--- End of stack trace from previous location where exception was thrown ---
   at System.Runtime.ExceptionServices.ExceptionDispatchInfo.Throw()
   at Microsoft.VisualStudio.ProjectSystem.CommonProjectSystemTools.Rethrow(Exception ex)
   at Microsoft.VisualStudio.ProjectSystem.ProjectErrorReporting.<>c__DisplayClass6_0.<SubmitErrorReport>b__0()
   at Microsoft.VisualStudio.ProjectSystem.ExceptionFilter.<>c__DisplayClass2_0.<Guard>g__action|0()
   at GuardMethodClass.GuardMethod(Func`1 , Func`2 , Func`2 )
```
   
*Exception 2*
![alt text](/Images/Exception2.png)


