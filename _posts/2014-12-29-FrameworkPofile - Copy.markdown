---
layout: post
author: "Ajay Narang"
title:  "Understanding .NET Framework Family and Profile"
date:   2014-12-29 10:57:22
categories: Articles DOTNET Framework

---

.Net has different flavour of runtime running in browser (Silverlight), Window Phones, Window Store, Window desktop 
and Xbox in other words different .NET Framework family.

Before Microsoft introduced VS2010, specifying project target framework was only limited to different framework version.
With VS2010 onwards .NET project not only target different version of framework but can also refers to different family and subset/profile.

So, VS2010 onwards Target framework is indicated by new moniker which is .Net framework Identifier, .Net framework version and .NET framework profile.

#Target Framework Moniker

Target Framework Moniker = Framework Identifier + Version + Profile/Subset.

Where, Framework Identifier refers to different flavour of .Net like Silverlight, Windows Store etc.
Version - .Net Framework version 
Profile – Subset of framework dictating certain area of application like .Net Framework 4.0 Client Profile.

Different tokens of Target Framework Moniker can be seen by viewing VS project file (.csproj/.vbproj) in notepad as shown below 

- Below project refers to Silverlight family of .Net Framework and version v5.0.

![Project File]({{ site.url }}/assets/DotnetProfile/Image1.png)
 
- Below project refers to client profile of .NET framework v4.0 , no identifier refers to desktop framework.

![Project File]({{ site.url }}/assets/DotnetProfile/Image2.png)

#Getting Target Framework Moniker Value 

Type the below command in Package Manager Console to see the target moniker value
$p = Get-Project "ProjectName"
$p.Properties.Item("TargetFrameworkMoniker").Value

#Target Framework and Referenced Assembly 

Target framework are design time concept, mostly used by VS and build machine to produce output which is guaranteed to run on the corresponding framework on any machine. 

It also dictates assembly, types or methods will be available to developer under that framework henceforth prevent developer from using any type/method which is not runtime prerequisite for their project. 

In VS2008 developers was prone to commit mistake by using method which may belongs other different version e.g. project with target framework v2.0 may use method written for v3.5 but with VS2010 .NET introduce concept called Referenced Assemblies restricting developer to use only assembly/types/methods corresponding to selected targeted framework.

##### *References Assemblies*

Reference Assemblies contain the type information and metadata for a target framework and do not contain any code. Generally, target framework is full framework like .NET Framework v4.0 but for some deployment scenario framework is not relevant like client application does not need asp.net assemblies/types to run.   Subset of full framework are call profile, profile never adds anything to framework rather it is just subset of full framework.

# Other references
- [Visual Studio Managed Multi-Targeting: Part 1](
http://blogs.msdn.com/b/visualstudio/archive/2010/05/19/visual-studio-managed-multi-targeting-part-1-concepts-target-framework-moniker-target-framework.aspx)
- [Visual Studio Managed Multi-Targeting: Part 2](http://blogs.msdn.com/b/visualstudio/archive/2010/05/26/visual-studio-managed-multi-targeting-part-2-multi-targeting-in-action.aspx)
- [Multi-Targeting Support (VS 2010 and .NET 4 Series)](http://blogs.msdn.com/b/visualstudio/archive/2010/05/26/visual-studio-managed-multi-targeting-part-2-multi-targeting-in-action.aspx)





