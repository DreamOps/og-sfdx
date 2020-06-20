# First Generation Packaging (1GP)

![(info)](info-16px.png) This guide covers the **First Generation Packaging** toolset (1GP).
 -   At some point, the new Second Generation Packaging would be covered here or in a companion guide.

---

**Top Tips**

 - [Be Mindful of Immutability](#be-mindful-of-immutability).
 - [Prototype with a Proxy Package](#prototype-with-a-proxy-package).
 - [Review New Components Before Upload](#review-new-components-before-upload).
 - **[Install New Versions to a Firewall Sandbox](#install-new-versions-to-a-firewall-sandbox). ![(star)](star-16px.png)** 
 -   [Renew Active Development Orgs Before They Expire](renew-active-development-orgs-before-they-expire).

See the full content for more about these tips.

---  

**The Salesforce Packaging Invocation**

- Grant to us the courage to change that which can be changed, the serenity of mind to accept that which cannot be changed, and enough documentation to know the one from the other.

---

# [Welcome](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_intro.htm)
![(info)](info-16px.png) Each heading on this page (like "Welcome") is a link to the corresponding section in the official Salesforce ISVforce Guide.

The  **Open Guide to SF Solution Packaging** is designed as an unofficial companion to the official **[Salesforce ISVforce Guide](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_intro.htm)**.

 - Each chapter in the Open Guide links to the corresponding chapter in the ISV Guide.

By following the links to the ISVforce chapters, you can orientate yourself to the base platform functionality.

 - The material offered in the Open Guide builds on the essential information provided by the Salesforce ISVforce Guide.

See also

 - [Salesforce ISV Onboarding Guide](https://na7.salesforce.com/5001H00000zFWexQAG)
 - [Partner Success Basics Webinar Series](https://partners.salesforce.com/s/education/appinnovators/Partner_Success_Basics_Series#z)


# [Quick Start](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/isv_intro_quickstart.htm)
"Learn to plan, build, distribute, market, sell, and support solutions that run on the Salesforce platform."

## Basics
This section is a primer to the Salesforce development infrascture. If the material is familiar, you can safely skip ahead to "Design and Build your App."

 - **Salesforce environments**  can be heavily customized by end users (and usually are).
  - Most local customizations can be packaged as a solution, or app, and distributed to other Salesforce customers.
  - By going through a Security Review process, these packages can be listed on the Salesforce AppExchange.
       -   The  [Salesforce AppExchange](https://appexchange.salesforce.com/)  works a lot like the Apple or Android stores.
        -   You can download solutions that extend your Salesforce environment, some of which are free, and others that are paid.
   - In 2015,  [license revenues from AppExchange apps](https://medium.com/understanding-as-a-service-uaas/demystifying-the-numbers-behind-salesforce-com-s-appexchange-60b3cedbc01f)  topped $1.5 billion.  _Nice!_
 - For development and testing, customers can clone the Salesforce production environment into a working "**sandbox**".
  - A production org comes with several sandboxes and more can be purchased.
  - Sandboxes can come with or without data. The ones with data come at an extra cost. With some difficulty, you can also import data yourself.
  - The platform provides various ways to move new features from a sandbox to its production org.
 - For **packaging** solutions, Salesforce provides a companion infrastructure, that uses either Developer Edition orgs or DX scratch orgs.
 - For customer trials, demonstrations, or development, ISV partners can provision new temporary orgs from a snapshot of a special source org using another infrastructure,  **Trialforce**.

## Caveats
Salesforce is a surprisingly transparent platform that puts great power in the hands of developers. 

 - And, of course, with great power, comes great responsibility!

### The Salesforce platform is deeply extensible
Customers have full access to a package's data schema and the storage of all standard data records.
 - For customers, this extensibility is a huge benefit, and it is a key driver for the immense popularity of Salesforce.
 - Ironically, for package developers, this same extensibility makes sweeping changes to our solutions more difficult to implement.
 - ![(info)](info-16px.png) Most or many of the  **Caveats**  in this open guide are a consequence of the platform's extensibility.
 - Working on a shared, multi-tenant platform is a significant  **paradigm shift**  for developers used to working on a standalone application hosted on private servers.
 - In practice, accommodating local extensibility is the  **cost of doing business**  on the highly collaborative Salesforce platform.


# [Design and Build Your App](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_designing_your_app.htm)
"Discover the architectural concepts that influence AppExchange solution design. Learn how to plan, build, and package your solution for customers."

## Basics
The Salesforce platform provides an architectural infrastructure with elements like Visualforce pages, Lightning components, SObjects, SOQL, Triggers, Apex Classes, and metadata, which you use to design and build your app.

### Architectural Assessment
Identify areas for improvement within your solution by asking yourself these questions. In each case, "Yes" is the right answer.'
- [Adapted from "Take Stock of Your Orgs Customizations" (Trailhead)](https://trailhead.salesforce.com/en/content/learn/modules/package-development-readiness/take-stock-of-your-orgs-customizations).
  
**Style**
Topics: General Conventions.
 - [ ] Observes your [Apex Style Guide.](https://nimbleuser.github.io/apex-style-guide/)

**Triggers**
Topics: Trigger patterns, Trigger logic.
 - [ ] Does your org have one trigger per object?
 - [ ] Is there  **no**  business or application logic written directly in a trigger?
 - [ ] Do triggers “hand off” logic or functionality to other classes (aka trigger handlers)?

**Apex Classes**
Topics: Naming conventions, Comments, API Version.
 - [ ] Do Apex classes use common prefixes or even namespaces to group units of code?
 - [ ] Do classes have similar names, based on functionality?
 - [ ] Is the purpose and authorship of code documented in comments?
 - [ ] Do classes have comments that help clarify function?
 - [ ] Do components use API version 24 or later?

**Apex Tests**
Topics: Test patterns/units, Code coverage, Test data handling.
 - [ ] How do tests relate to other code?
 - [ ] Does each class have its own test?
 - [ ] Are tests organized into functional groups?
 - [ ] Are all parts of your code base covered by tests?
 - [ ] Do tests depend on common data factories or static resources?
 - [ ] Do all of your tests  **not**  use the 'seeAllData=True' annotation, and run on API version 24 or later?

**Lightning Components and Events**
Topics: Naming conventions, Comments, Apex controllers, API Version.
 - [ ] Do components use common prefixes or even namespaces to create groups?
 - [ ] Do components have clear names, related to functionality?
 - [ ] Are Lightning events scoped to be application events or component events?
 - [ ] Are the purpose and authorship of components and events clearly documented in comments or Aura documentation files?
 - [ ] Do components use Apex controllers?
 - [ ] Do components use API version 29 or later?

**Visualforce**
Topics: Naming conventions, Comments, Apex controllers, API Version.
 - [ ] Do Visualforce pages and components use common prefixes or even namespaces to create groups?
 - [ ] Do pages have clear names, related to functionality?
 - [ ] Do pages use Apex controllers?
 - [ ] Do pages use API version 24 or later?
 - [ ] Are  **no**  pages used with email templates?

**Objects**
Topics: Dependencies.
 - [ ] Do  **any**  objects implement a master/detail relationship between a standard and custom object.

## Tips - Design
Creating a solution that plugs-into Salesforce is a very different experience than designing a solitary .NET solution. #WelcomeToTheJungle!

### Adjust your Expectations
When Salesforce designed first-generation packaging (1GP), it seems that the first priority was protecting the subscriber, even if that meant simplifying the packaging tools.
 - As a result, the 1GP model does not always follow what many people would consider common industry practice for solution versioning and packaging.
 - Of course, many of those practices evolved for standalone solutions, and they do not consider the needs of a solution that plugs-into a highly extensible and transparent environment.

### Adopt a Style Guide
One example of a style guide is the [the NimbleUser Apex Style Guide](https://nimbleuser.github.io/apex-style-guide/). 
 - Feel free to use this one, or roll your own.

### Avoid Master/Detail Relationships between a standard object and a custom object.
These relationships can't be packaged with a permission set, and they can present performance issues.

### Data Storage Costs
Salesforce charges by the row and not by the number of bytes stored.  [For cost purposes, each row is allocated a flat 2kb, 4kb, or 8kb, regardless of the actual row length](https://help.salesforce.com/articleView?id=000318951&type=1&mode=1).

### Field Lengths
As a consquence of [Data Storage Costs](#data-storage-costs), you can err on the side of longer fields without driving up your storage costs.

### Normalization
As a consquence of [Data Storage Costs](#data-storage-costs), if you over-normalize your data schema, you can drive up data storage costs, since a by-product of heavily normalize schemas is more rows.

### Assisting with Data Import
Include an  [External Id field](https://help.salesforce.com/articleView?id=000320964&type=1&mode=1)  on each of your objects so that customers can use it when importing data.

### External IDs
When creating a text field for an External Id for customers to use, it's helpful to use the full 255 character length.  
 - Declaring the full length doesn't cost us anything and someone may need it later.

## Tips
Salesforce architecture is continually improved and refined, season by season.

### Consider Feature Management
Using  [feature management](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/fma_manage_features.htm)  you can create "[software toggles](https://en.wikipedia.org/wiki/Feature_toggle)" in your Apex code to hide new capabilities (thereby separating deploying from releasing).
 - When coupled with permission sets, feature management allows you to "dark launch" features.
 - Package developers also use feature management to enable extra-cost features.
### Document your API
Apex has its own version of Java Docs that live in you with  **[Apex Doc](https://github.com/SalesforceFoundation/ApexDoc)**  that live in your code.  
 - A **webhook** in your version control system can be used to to regenerate the docs.
 - The generated Apex Doc content is static HTML and easy to host in a  **S3 bucket**.

### Empty Lists are DML No-Ops
When a data operation is passed an empty list, the operation is  _not_  performed on the empty list. In the following example, when  `recordsToUpdate`  is empty, the following two commands are equivalent, with the second form preferred. (Some time ago, the first form was preferred, but the platform is smarter now.)
 - if( !recordsToUpdate.isEmpty() ) { update recordsToUpdate; }
 - update recordsToUpdate;

### Free to Paid
If you start out with a free app, and then decide to to bring out a paid version, you can position the paid version as an extension to the base free app.
 - Of course, the paid extension will need to pass the Security Review and the usual fee will apply.
 - See also  [Publishing Extensions to Managed Packages](https://help.salesforce.com/articleView?id=publish_extensions.htm&type=5)  in Salesforce Help.
 - Even better,  _Consider Feature Management_  (see Tips - Architecture). 

## Caveats
Salesforce uses a multi-tenant architecture, and we need to make special effort to be a good neighbor.

### RTFM
To protect multi-tenancy, the platform has a number of well-documented allocations and limits. There are also a number of considerations when packaging components. For starters, be sure to study these key resources:
 - [Salesforce Features and Edition Allocations](https://help.salesforce.com/articleView?id=overview_limits_general.htm)
 - [Salesforce Developer Limits and Allocations Quick Reference](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_overview.htm)
 - [Components Available in Managed Packages](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_packageable_components.htm)

### Aloha Limits
Lightning apps, custom apps, and custom tabs --  _**only**_  – don’t count against the allocations for the subscriber's org only when in a managed package that’s passed Security Review .
 - All other component and runtime limits apply, including components like Custom Report Types.

This point is mainly a limitation for **Professional Edition**, which has lower limits for several components, such as permission sets and flows.

### Apex Test Tour
 Just as a gripe: No matter how many years and how many times you run the Apex tests in an org, every so often the system will ask you if you want to take the guided tour.


# [Package and Test Your Solution](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_testing.htm)
"Learn how to package, upload, and install a beta version of your solution as part an iterative development approach. After your beta is up and running, learn how to test, fix, extend, and uninstall the solution."

## Tips
Packaging a Salesforce solution may seem daunting at first. In practice, the process is consistent, repeatable, and reliable.

### Checklists Are Your Friend
Successfully designing, packaging, testing, distributing, supporting, and upgrading Salesforce solutions can be an intricate mixture of your own processes and steps mandated by the platform. Developing a set of checklists can go a long way toward making this elegant dance a repeatable, teachable process. 'Nuff said.

### Policy Statements
A good companion to a set of checklists is a page outlining your packaging policies, the simpler the better.

### Consider Namespaces Carefully 
Each package has a full-name, description, and namespace. The namespace is mainly for developer use, but it is shown on the Installed Packages page. The full-name and description can be updated, but the namespace is permanent and can never be changed.
 - Review how other packages approach namespaces, and consider developing a style guide for namespaces before creating your first package. – It's rarely your last.
 - Remember there are a lot of packages sharing a 15-character range for namespaces. It's unlikely you will be able to claim anything short and obvious.
 - Apex is suppose to be case-insensitive, but there are spots where the namespace is expected to be rendered in upper case.
     - ![(help)](help-16px.png) Consider using upper case when you first specify the namespace in your Developer Edition packaging org.

### On an Object, Don't Package an "All" List View
If you do, then subscribers are faced with two "All" list views, the original implicit All list view and the one from your package. The list views are subscriber deletable, so it's a quick fix on the customer side, but, it's not a professional look for your solution.

### Take Care When Packaging Permission Sets and Designing Profiles
There are restrictions around packaging permissions. The Salesforce Help pages indicate what can be packaged, but, for the most part, do not indicate what  _cannot_ be packaged.
 - If you include a grant in your package that is not permitted, the grant is silently dropped. You won't know it's not working until you try it.
 - One example is that  **System Permissions**  cannot be packaged, but you may want them to allow people to run flows.
	 - One workaround is to ask subscribers to create the permission set with the System Permission themselves.
     - Alternatively, if you have a user account with the subscriber's org, or, better yet, a connected app, the permset can be deployed directly as unmanaged code.
     - Another example is that you can't package  **Record Type Visibilities**  in permission sets, and so you have to leverage profiles for record type settings.
     - In both cases, the documentation does omit these component type from the list of what can be packaged.
 - ![(warn)](warn-16px.png) The page does not detail what  _cannot_  be packaged, and it's not clear why a table is not used to format the information.

See also [Permission Sets and Profile Settings in Packages](https://help.salesforce.com/articleView?id=distribution_perm_sets_profile_settings.htm&type=0) and [Permission Sets Considerations](https://help.salesforce.com/articleView?id=perm_sets_considerations.htm&type=5) in Salesforce Help.

### Prototype with a Proxy Package
True betas can be problematic since they cannot be upgraded.
 - A more useful approach is to create a second, proxy package under another namespace, and deploy your code to the proxy package first.
 - Ideally, reserve your preferred namespace in a Developer Edition org, and fully develop the initial version in another "proxy" packaging org, under a different namespace.
 - Automate uploading the package on at least a nightly basis. Some Apex Tests only fail during the package upload process, often for namespacing issues.
 - Conversely, some tests will fail locally and pass during upload, especially those hitting a CPU timeout. 
	 - Then after uploading and testing the proxy, time and again, when all seems well, deploy the same code to your "golden copy" org, and upload it under the customer-facing, production namespace.
     -  Continue to develop new major versions first using the proxy, and then switching to the golden copy for a release candidate.

### Semantic Versioning
Salesforce provides three digits for a version but only requires use of two. The other digit can be used to implement [semantic versioning](https://semver.org/), to indicate a change in dependencies or such.
 - **1.2.3** Salesforce uses digit 2 and 3, but never touches digit 1. You can advance the first digit whenever there is a significant semantic change to your package.

### Seasonal Versioning
Another use is to indicate your own seasonal version in the leftmost digit. Under this approach you can bring out several major versions as release candidates, without rolling the leftmost digit more than once.
 - 20.3.0 - Winter
 - 21.2.0 - Summer
 - 22.5.0 - Spring

### Review New Components Before Upload
First, make sure component names meet your style guide standards. Second, if you haven't packaged a component type before, review the considerations before jumping in. Components like Flows and Custom Report Types, among others, have restrictions that you might not expect. See Caveats.
 - When uploading, Salesforce doesn't itself provide a new component list, though here is a Gist that scrapes the Package Details page:  
	 - [Gist](https://gist.github.com/TedHusted/b4981225284e9ee4fdad536b3fbdc027)

### Review New Dependencies Before Upload  
If you are using the Upload Form, the dependencies are conveniently shown at the end of the form. Just remember to look!
 - If you use a proxy package, with automatic uploads, you can check the dependency afterwards by opening the Package Details page and clicking the Dependency button.
 - The presentation here is more detailed (and less convenient) than the presentation on the Upload Form.
 
### Standup a Technical Change Log for Each Version
The technical change log should indicate which tracker issues were merged into source control (such as Jira issues), the new components being added, and any new dependencies.
 - The change log is also a good place to indicate any manual upgrade steps, such as deleting an Apex class or other component, or changes a local administrator might need to make.
 - Often upgrade steps can be captured in the tracking issue.
 - If you have indicated an issue tracker ID in every commit, you can use a pull request to determine what issues are being merged.
   - If you are using Jira and Confluence, it's easy to put a Jira macro on Confluence page, and then filter by the fixVersion. Bitbucket also automatically links Jira IDs to the underlying issue.

### Organize by Release
Rather than keep different "types" of documents together, consider keeping all of the documents for a given release together. 
 - Often questions might arise about a past release, and it's convenient to have all of the related documents together. 
 - (A similar idea is to keep all your tax records for each year together – as opposed to keeping all the bank statements together in the same file year-after-year.)

### Use Mocks in Apex Tests
Implement mocks to streamline test run time, both to accelerate development and also to reduce upload time.
 - [Work Around UNABLE_TO_LOCK_ROW False Negatives](https://nawforce.blog/2019/06/09/parallel-unit-testing-via-sfdx-cli/)  (Kevin Jones)

### Install New Versions to a Firewall Sandbox
In the event of a real emergency, you can undo a major release by  [reverting your managed package to a beta version](https://help.salesforce.com/articleView?id=000312548&language=en_US&type=1&mode=1). But to be reverted, the version cannot be installed in any org whatsoever. By upgrading a sandbox first, you can catch the worst errors while it's still easy to refresh and revert.

### Firewall Regression Tests
If your solution exposes any global components, be sure to run tests against the global API from outside the package. This step will quickly catch any anomalies, which you can still revert and rework new global components.
 - The simplest approach is to copy the Apex Tests that exercise the global members from within the package, so that they invoke the global members from outside the package – the way your extensions or subscribers will do.
 - A more effective approach is to document your Global members with  **[Apex Docs](https://github.com/SalesforceFoundation/ApexDoc)**, and then develop a set of Apex Tests that validate what's promised in the Apex Doc content.

### Test Against the Next Version
During the seasonal rollouts (October/February/June), the upcoming version is available, giving you the opportunity to test against both the current and preview versions.
 - There are three ways to access the upcoming release during the rollout period.  
	- **Sign-up for the Pre-Release**  -  Google "**Salesforce Pre-Releas**" and look for the upcoming season.
	    - If you signup for a Developer Edition, the org will persist into the next release and be upgraded automatically.
     - **Use a preview sandbox**  on a test or customer org
	     - Google: "**Salesforce Sandbox Preview**" and look for the upcoming season.
     - **[Select the Salesforce Release for a Scratch Org](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_scratch_orgs_version_selection.htm)**  during the preview period.

## Caveats
Today, many packaging decisions cannot be undone, and so it's important to take care and study the process.

### Namespaces are Forever
The namespace assigned to a managed package can never be changed. See also Tips.
  - ![(info)](info-16px.png) Object and other component names are tied to the namespace, making changing the namespace reference non-trivial, as local customization may also reference the namespace.

### Be Mindful of Immutability
Once a version is released, global method signatures cannot be changed; global classes and most other components cannot be removed.  
 - ![(info)](info-16px.png) Global scope is intended to be used by consumers of your package: local customizations and extension packages (which would immediately be broken if the global signatures change).
	- See also:  _Install New Versions to a Firewall Sandbox_.
* **Do not promote a member to global**  unless it  **_absolutely_  and  _positively_**  has to be global for  **_other_**  people to use your package, and you have no other choice.
    -   Global scope is  **not**  needed simply because your class is a batchable implementation, or some such.
         -   ![(warn)]warn-16px.png) Global scope is  **only**  needed to call a member from  _outside_  your package.
    - Global immutability extends to interfaces as well, which can sometimes be a surprise.

### Avoid the Salesforce  [Deprecation annotation](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_classes_annotation_deprecated.htm) 
If a global should not be used, raise an exception instead instructing the consumer as to what to do instead.  
 - If you mark an existing class as deprecated with the annotation, and upload it as part of your package, two things happen:  
    1. That method cannot be used in  **new**  subscriber orgs, but it remains visible to orgs that had the earlier version of the package installed, before it was deprecated.  
    2. It becomes impossible to make later changes to this class's content.         
 - The second point can be a foot-shooting moment since it's  _**irreversible**_, to the extent that it also becomes impossible to fix pre-existing bugs in the deprecated code.
 - The lesson is that before creating a global, you should be sure that you have a way to communicate changes to your stakeholders, and avoid shackling yourself to obsolete code with the deprecated annotation.

### One and Done
Some components can be removed after release – and many others cannot. See  [Components Available in Managed Packages](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_packageable_components.htm)  for details.  
 - You may be able to use a  **Remove**  link from the  **Package Details page**, or you may have to delete it from the packaging org.
 - To delete a component from a package, Salesforce Support will need to enable component deletion for you.         
 - It seems like fewer components are deletable, and most newbies need to be cloned to be subscriber editable.  
    - ![(info)](info-16px.png)  Once a component is cloned, it it not upgradeable, and so subscribers may need to manage their own updates.
 - Once a packaged component is deleted,  **the API Name can never be used again**  in the packaging org.  
    - ![(info)](info-16px.png)  Allowing the package to create another component with the same name could conflict with local installs that have the prior component.
 - Some people will leave an Apex class and just empty it out, so they have the option of using the same name again.
 - Other people delete the obsolete component, and if it's wanted again then append an integer to the API Name ("API_Name2") and set the user-facing label any way you like.      
    - ![(info)](info-16px.png) Automatically deleting visible components (like Custom Fields and Record Types) could break local customizations, so they are left in place, but detached from the package, and left in a deletable not not-editable state.
  - The package-removed components can be deleted manually from Setup in the Subscriber's org as per customer's business requirements.
 - ![(info)](info-16px.png)  Package-removed master/detail indexes have been known to cause performance issues if not deleted.
    - ![(warn)](warn-16px.png)  Some components might be included automatically through dependency resolution, and once packaged, some components cannot be removed.  
 - See also _Review New Components Before Upload_.

### No Rollbacks
Once a new version of a package is installed, you cannot simply "rollback" to the prior version. You can either uninstall the package and reinstall a prior version or roll-forward to another new version. If the package stores data, uninstalling is disruptive, and so we generally roll-forward to correct an issue.
 - ![(info)](info-16px.png) Once the new version is installed, customers can take advantage of new features, and rolling back the version could break local extensions.

### Apex Tests Limit Upload Time
The platform runs all of your package's Apex Tests on each and every upload, one at a time. For larger packages, with thousands of Apex tests, uploads can take several hours to complete. (In an extreme case, one developer reports that uploads for their package can take  _days_  while the tests run.) The only mitigation (for first generation packaging) is to work hard to keep your tests running fast, or use extension packages to modularize your code.
 - **Net-new projects** that expect to grow should consider Second Generation Packaging (2GP) since it's modular by design.

### Uploads cannot be cancelled
Once the upload starts, it can't be cancelled. It often runs to the end even if a test fails.
 - ![(warn)](warn-16px.png) It's unclear why an upload cannot be stopped.
  
### Apex Test False Failures
When run concurrently, it's commonplace for valid Apex tests to fail, often due to row locking issues. If you are running the Apex tests interactively, a good approach is to run the tests in concurrent mode first, and then run the failed tests asynchronously (one-at-a-time mode). Here's a bookmarklet you can run from Chrome to select the tests which failed in the last run. First, open the Select Test dialog in the UI, and then launch the bookmarklet.

`javascript:``for``(``var`  `a=document.querySelector(``".x-grid-group"``).querySelectorAll(``"img.Failed"``),b={},c=0;c<a.length;c++){``for``(``var`  `d=a[c];``"TR"``!==d.nodeName;)d=d.parentNode;b[d.querySelector(``"a"``).nextSibling.textContent.trim().replace(/\w+\./,` `""``)]=!0}``for``(``var`  `f=document.querySelectorAll(``"#testOverlay .x-grid3-row:not(.x-grid3-row-selected)"``),c=0;c<f.length;c++){``var`  `g=f[c].querySelectorAll(``"td"``);b.hasOwnProperty(g[1].textContent)&&(e=``new`  `MouseEvent(``"mousedown"``,{bubbles:!0}),g[0].querySelector(``".x-grid3-row-checker"``).dispatchEvent(e))};`

# [Pass the Security Review](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/security_guidelines.htm#security_guidelines)
"At Salesforce, nothing is more important than the security and success of our customers. To distribute a solution on AppExchange, it must pass our comprehensive security review. Learn how to design a solution security strategy and prepare for the security review."

## Tips
The security review process is well documented but still mysterious in its own way. 

### Start with your most minimal, minimal viable product
As soon as the package is approved, you can bring on successive upgrades to improve on your MVP.
 - Salesforce does run automatic scans on your package, but they do **not** require you to submit every new version for another in-depth security review.


# [Publish Your Offering on the AppExchange](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_distributing.htm)
"You turned an idea into a solution and are ready to get it in front of customers. To publish your solution on AppExchange, use the AppExchange publishing console. The publishing console is where you create a listing for your solution, connect orgs, manage license settings, and view analytics for your published listings."

## Basics
After all the other hard work, be sure to put your best foot forward!
 - [Salesforce Partner Field Guide the Perfect AppExchange Listing](https://www.appexchangeguides.com/i/1175814-salesforce-partner-field-guide-the-perfect-appexchange-listing/1)  (Partner link)
 - [Build Apps as an AppExchange Partner Trail](https://trailhead.salesforce.com/content/learn/trails/isv_developer_beginner)
 - [ISVforce Guide](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_intro.htm)

## Tips
Salesforce is a subscription service, and publishing is a ongoing process. 

### Submit and Resubmit
To keep your AppExchange listing current, you need to resubmit the package for security review.
 - When you submit the form, using the Security Review wizard, the listing is then updated with the current version and date.
 - A full security review is **not** automatically triggered by taking this step.
    - Of course, Salesforce can review your app at any time and insist that security fixes be made when warranted. So, be prepared!  
    - _Salesforce advises:_ "The Security Review team reserves the right to recall any application for manual review again. So it's advisable that you have a strong change management process in place so all new changes will be secure. This way, you'll be ready when (not if) re-review happens."
 - To update the version and release date on your listing, you still need to go through the steps of applying for security review and have an org ready for review. The org is the tedious part.

See also the aforementioned tip: _Use a TSO for Ongoing Security Reviews_.

### Use a TSO for Ongoing Security Reviews
If you plan to keep your listing current, it can be worthwhile to setup a Trialforce Source Org to use with the security reviews. You can then spin off trials when you submit for an updated review.


# [Manage Licenses](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_manage_licenses.htm)
"Learn how to use the License Management App (LMA) to manage leads and licenses for your AppExchange solutions, and how to provide administrative support for your customers."

## Tips
The LMA can provided a wealth of information about your subscribers.

[Associate Your Package with the License Management App](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/lma_associate_package.htm)
- Among other things, you can use the Subscriber Console to debug issues with your package that are occurring in a subscriber's org.
 
### Register pre-certified packages with your LMA
If you need to use the Subscriber Console for debugging, and your package hasn't been submitted for Security Review yet, you can still link it to your LMO, by following the usual process.

### Supplement LMA Record with Org Details SObject
The platform creates a License record for each version installed. While the detail is welcome, finding the current record can be difficult, and you may wish to track other details about the customer's org. (Technically you could extend the LMA record, but modifications to the License object are not recommended.)
 - Design an "Org Details" SObject to track the most recent license version and to store supplemental details.
 - Link the Org Details to the customers Account record, to maintain a 360 degree view.
	 - If the org is for internal use, link it to your own Account record.

### Consider LMO Add-Ons: App Analytics and App Cockpit
   - **App Analytics**  provides usage data about how subscribers interact with your AppExchange solutions. App Analytics requests are submitted via SOAP API. This App will allow an ISV to submit their requests directly within their Licensing Org.  [See the AppExchange Listing for details.](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000G0nUXUAZ)
   - **App Cockpit**  is an open source solution, offered by a leading member of the ISV community, that automatically reports on the uncaught exceptions raised by your package. It  and helps you monitor the health of your apps and proactively support your subscribers when errors arise.  [See the Demo Video on YouTube](https://www.youtube.com/watch?v=GTy0Lr19z34).


# [Provide a Free Trial of your Solution](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/trialforce.htm)
"Maximize customer adoption by offering free trials of your solution on AppExchange. Explore the types of trials available and determine the best type for your solution."

## Caveats
Trials are a great way for subscribers to test-drive your product, but there are a few potholes to navigate.

### Salesforce IDs
 If the content of a field appears to be a Salesforce ID, Salesforce will quietly replace it with a new ID. This behavior is actually a feature. Consequently, if you include Salesforce IDs in your data records (say for use as an External ID), you need to change them in some way. One approach is to append a hashtag sign ('#').

### TSO Limits
 A few limits on TSOs are lower than you will find on paid-for Enterprise Edition orgs.

### Trialforce Pivot Date
The TSO has a great feature for keeping the date fields in your Trial org current. Sadly, you can't control the pivot date: it's hardcoded to the creation date of the TSO.    
 - ![(help)](help-16px.png) If you populate your TSO with sample data that includes dates, create the TSO on January 1st, or the first day of a quarter, to simplify the date arithmetic.

### Renew Active Trial Orgs and Trialforce Source Orgs Before They Expire
Except for Developer Edition orgs, all Salesforce orgs expire within a year, including Trialforce Source Orgs.
 -  The customer production orgs, Salesforce handles as part of the license renewal. Any orgs you use for testing or development are your responsibility. Be proactive!
        - ![(info)](info-16px.png) The org renewal date is not indicated on the **Company Information** page, and so it's something we need to track ourselves.
 - For partners, extending an org is blazingly easy. File a case within 30 days of the expiration, and a few minutes later, the extension is processed.
 - But you still have to file the case, and it helps to know the Org ID.
 - Once you are past the renewal date, you are locked out, so know your Org ID.
  - For our standing orgs, we renew them all set to the same date, with the list of Org IDs on a recurring event on a shared calendar. Then we file all the cases at once, rat-a-tat-tat.
   - Another good idea is to scan the LMA for org expiration dates. Let us know if you have implemented something like this!
 - **As to Developer Edition orgs,** if you stop using the org, you'll get an annual notice asking you to sign-in to keep it going.
	 - [Your DE org] has been inactive for the past 365 days.  
    Due to capacity planning best practices, we are locking DE orgs that have been inactive for 6 months or more. If you want to continue using your DE org, simply log in before  [next month].  If you do not wish to continue using your inactive DE org, no action is required.
 -  What if I don't take action?
	- If you don't login, the org will be locked on [next month] and then deleted after 30 days.  You can reactivate a locked org by opening a case with Customer Support via the Help & Training portal.  Once an org has been deleted, it cannot be reactivated.

      
# [Update Your Solution](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_upgrading.htm)
"Your packaged solution is ready for an update. Learn how to fix small issues with patches and make major changes with upgrades."

## Basics
**Automatic Updates** are available through push upgrades. Be sure to see  [Best Practices for Push Upgrades and Patch Versions](https://help.salesforce.com/articleView?id=push_patch_best_practices.htm&type=5) (Salesforce Help)

### Patch Orgs
Use a patch org to maintain the current customer-facing version so that the main package can publish new internal-facing major versions (milestones) before the next new customer-facing versions.  
 -   Each package can have exactly one new major version (under 1GP).
     - Each major version can have exactly one series of patch versions.
 -   No new components can be added to patch versions (including Labels).
   
## Tips
Upgrades are a great way to provide new value to your subscribers. 

### Check Known Issues
Sometimes a support incident can be traced back to a known issue with the Salesforce platform. Patches are applied regularly, and so there is a ongoing break/fix cycle between seasonal releases.
 - See **[Salesforce Known Issues](https://success.salesforce.com/issues_index)**  on success.salesforce.com

### Retain Backwardly Compatibility
 - **Required fields** must not be added to released managed objects, since it will prevent saving existing records without intervention by the operator.
 - If desired, the field may be instead required on the  **page layout**  and presented as an upgrade step for the local administrator.

### Consider Following a Pilot/Beta/GA Pattern
Salesforce often introduces new features to a select group using a Pilot program, which is followed by an opt-in Beta, and finally a GA version that anyone can use.
 - If you are rolling out a feature with a dependency on a new Salesforce feature, it can help to stay a step behind.
 - When Salesforce releases the Beta, you release a Pilot. When Salesforce goes GA, you bring out a Beta, then your own GA version with the next major version.
 - In this way, you give Salesforce a chance to refine the new feature, while still moving forward with your own extension.

### Adopt New Salesforce Capabilities
Salesforce is a moving target, and you need to move with it. You may not want to embrace the  _first_  GA version of a new capability but don't let a full year go by either.

### Provision a DE Pre-Release Org
Every season, Salesforce publishes a pre-release version. If you order a pre-release using a Developer Edition org, Salesforce will automatically update the org in subsequent seasons (becomes DE orgs don't expire). You can then install and update your package for early testing, and keep using the same org, season after season.

### Understand How to Remove Visualforce Pages
There is a  [documented two-step process](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_managed_component_deletion.htm)  that you need to follow to remove a Visualforce Page from your package properly.
 - ![(warn)](warn-16px.png) Be sure to heed the warnings, or you will scuttle your upgrade path.

### Consider Not Removing Obsolete Components
While there are components that you can remove from a managed package, consider leaving them in place. You can update the component label to indicate that it's no longer used, remove the component from your profile settings or permission sets, and ask local administrators to do the same.
- _Even if you remove the component,_  it is left behind in the orgs where it was installed (except for public Apex classes), until a local administrator deletes it.

### Upgrade Extension Packages Only When Necessary
During milestone development, it is safer to withhold upgrading the base package in an extension packaging org unless the version is needed to deploy the latest code to the extension packaging org.  
 - ![(info)](info-16px.png) Once an extension package dependency is updated, it can be impossible to revert the base package to beta without destroying the extension package.
 - When all customers have been upgraded to a given base package version, then it becomes safe to bring the extension packaging org up to the same version.  
        
### Track the Partner Alerts
Salesforce publishes regular alerts to be sure partners are ready for upcoming changes. It's a good idea to assign someone to watch the alerts and track whether you are affected by each alert, and, if so, your response.
 - See [Partner Community News Events](https://partners.salesforce.com/partnerNewsEvents) (partners.salesforce.com).

## Tips - Patch Versions
Maintenance releases can be a great way to keep subscribers happy, so long as all the changes are kept in sync.

### Review the Salesforce Versioning Scheme
With First Generation Packaging (1GP), [Salesforce uses a simple versioning scheme](https://developer.salesforce.com/docs/atlas.en-us.packagingGuide.meta/packagingGuide/packaging_patches_about.htm) that supports a Major Version and Patch Versions (and nothing else).
 - Each patch version should have its own branch in version control, carefully created from the same commit as its major version.
     - Be sure to test a patch org  **before you need it**  by deploying the unmodified branch and uploading a beta.
         - ![(warn)](warn-16px.png)  Things can go bump in the night, and before a patch org can be used, you may need to file a support case to fix some new issue.
 - The best practice is to fix the major version first, and then cherry-pick to the patch branch.
    - Sometimes rework is required to omit new components, but the patches are essentially one-way forks, so internal changes can be made to classes.
 - Second Generation Packaging has more flexibility, but 2GP is currently out of scope for this document.

### Confirm Patches with an Affected Customer
Fixes that we patch out to the current release are usually created using internal development environments. If the fix is reported by a specific customer, it can be useful to upgrade that customer's org (preferably a sandbox) first – just to be sure the fix actually resolves the issue.

## Tips - Distributions
As you gain more subscribers, managing upgrades becomes a good problem to have.

### Track Releases as an Issue
If you follow a multi-step process after uploading a release, track it as an issue with Jira, or whatever tracker you use.
 -   On an  **Agile Board**, the columns will have different headings, but the process works well, as getting a new version out to customer might mean either multiple hand-offs or other multiple stages.

### Consider Custom Tooling
For larger distributions, it can be worthwhile to create your own push upgrade tooling using the API Salesforce provides.
 - See also [Using Push Upgrade API to Automate Package Upgrade Process](https://medium.com/inside-the-salesforce-ecosystem/using-push-upgrade-api-to-automate-package-upgrade-process-c9e2ff4cb8df) (Medium).

### Upgrade Access via a Connected App
If your customer relationship permits the use of a connected app, you can also consider "pull" upgrades using the metadata API.
- If you do have connected app access, there is a range of upgrade steps you can automate that can't be done using a package install.
- If you develop your own pull upgrade tooling, AWS EC2 is a good way to scale up and run hundreds of upgrades concurrently.

**Bookmarklet to provision EC2 instances**

`javascript:(``function``(){``if``(``"forge.nimbleams.com"``!==window.location.host)alert(``"You must run the bookmarklet at forge.nimbleams.com"``);``else``{``var`  `b=prompt(``"Number of agents?"``),c=parseInt(b,10);c.toString()!==b?alert(``"You must enter a number"``):fetch(``'/crumbIssuer/api/xml?xpath=concat(//crumbRequestField,":",//crumb)'``,{credentials:``"same-origin"``}).then(``function``(a){``return`  `a.text()}).then(``function``(a){``var`  `b=a.split(``":"``);alert(``"Please wait and do not close or reload this tab"``);a=Promise.resolve();``for``(``var`  `d=0;d<c;d++)a= a.then(``function``(){``return`  `fetch(``"/cloud/ec2-hosting.nimbleams.com/provision"``,{method:``"POST"``,headers:{``"Content-Type"``:``"application/x-www-form-urlencoded"``},body:b[0]+``"="``+b[1]+``"&template="``+encodeURIComponent(``"(default) Ubuntu Server 16.04 LTS (HVM), SSD Volume Type "``)})}).then(``function``(a){``if``(!a.ok)``throw`  `Error(``"Request failed"``);});``return`  `a.then(``function``(){``return`  `alert(``"Done provisioning agents"``)})})[``"catch"``](``function``(a){``return`  `alert(a)})}})();`
