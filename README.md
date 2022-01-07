[comment]: # "Auto-generated SOAR connector documentation"
# Terraform Cloud

Publisher: Splunk Community  
Connector Version: 1\.0\.11  
Product Vendor: HashiCorp  
Product Name: Terraform Cloud  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.8\.24304  

This app integrates with Terraform Cloud to perform generic and investigative actions to manage runs, plans, and applies

[comment]: # " File: readme.md"
[comment]: # "  Copyright (c) 2020 Splunk Inc."
[comment]: # ""
[comment]: # "  Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""
# Authentication

All requests must be authenticated with a bearer token. Use the HTTP header Authorization with the
value Bearer {token}. If the token is absent or invalid, Terraform Cloud responds with HTTP status
401 and a JSON API error object. The 401 status code is reserved for problems with the
authentication token; forbidden requests with a valid token result in a 404. There are three kinds
of token available:

-   **User tokens** — each Terraform Cloud user can have any number of API tokens, which can make
    requests on their behalf.
-   **Team tokens** — each team can have one API token at a time. This is intended for performing
    plans and applies via a CI/CD pipeline.
-   **Organization tokens** — each organization can have one API token at a time. This is intended
    for automating the management of teams, team membership, and workspaces. The organization token
    cannot perform plans and applies


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Terraform Cloud asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  optional  | string | Terraform URL \(e\.g\. https\://app\.terraform\.io\)
**ph1** |  optional  | ph | Placeholder
**token** |  required  | password | Authentication Token

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[list workspaces](#action-list-workspaces) - Lists workspaces in the organization  
[list runs](#action-list-runs) - Lists runs for a workspace  
[create run](#action-create-run) - Create a run which will perform a plan and apply  
[create workspace](#action-create-workspace) - Create a workspace within Terraform  
[apply run](#action-apply-run) - Applies a run that is paused waiting for confirmation after a plan  
[get apply](#action-get-apply) - Get details of an apply  
[get plan](#action-get-plan) - Get details and status of the plan of a run in Terraform  
[get run](#action-get-run) - This endpoint is used for showing details of a specific run  
[get workspace](#action-get-workspace) - Get details of a workspace  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'list workspaces'
Lists workspaces in the organization

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**organization\_name** |  required  | Name of the organization to list the workspaces of | string |  `terraform organization name` 
**page\_num** |  optional  | Page number of workspace list | numeric | 
**page\_size** |  optional  | Number of workspaces to return per page \(100 is default\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.organization\_name | string |  `terraform organization name` 
action\_result\.parameter\.page\_num | numeric | 
action\_result\.parameter\.page\_size | numeric | 
action\_result\.data\.\*\.meta\.pagination\.prev\-page | string | 
action\_result\.data\.\*\.meta\.pagination\.next\-page | string | 
action\_result\.data\.\*\.meta\.pagination\.current\-page | numeric | 
action\_result\.data\.\*\.meta\.pagination\.total\-pages | numeric | 
action\_result\.data\.\*\.meta\.pagination\.total\-count | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.applied | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.discarded | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.none | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.applying | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.cost\-estimated | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.plan\-queued | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.policy\-checked | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.cost\-estimating | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.confirmed | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.policy\-soft\-failed | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.policy\-override | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.canceled | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.apply\-queued | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.planning | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.planned | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.policy\-checking | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.errored | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.total | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.pending | numeric | 
action\_result\.data\.\*\.meta\.status\-counts\.planned\-and\-finished | numeric | 
action\_result\.data\.\*\.data\.\*\.relationships\.organization\.data\.type | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.organization\.data\.id | string |  `terraform organization name` 
action\_result\.data\.\*\.data\.\*\.relationships\.latest\-run\.data | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.current\-run\.data | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.current\-state\-version\.data | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.operations | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.environment | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.source\-name | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.locked | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.name | string |  `terraform workspace name` 
action\_result\.data\.\*\.data\.\*\.attributes\.auto\-apply | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.terraform\-version | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.description | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.created\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.vcs\-repo | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.actions\.is\-destroyable | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.queue\-all\-runs | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.source | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.latest\-change\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.working\-directory | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.source\-url | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.file\-triggers\-enabled | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.speculative\-enabled | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-destroy | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-lock | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-force\-unlock | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-queue\-apply | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-queue\-run | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-read\-settings | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-unlock | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-update\-variable | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-queue\-destroy | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-update | boolean | 
action\_result\.data\.\*\.data\.\*\.type | string | 
action\_result\.data\.\*\.data\.\*\.id | string |  `terraform workspace id` 
action\_result\.data\.\*\.data\.\*\.links\.self | string | 
action\_result\.data\.\*\.links\.next | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.links\.prev | string | 
action\_result\.data\.\*\.links\.last | string |  `url` 
action\_result\.data\.\*\.links\.first | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list runs'
Lists runs for a workspace

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Name of the organization to list the workspaces of | string |  `terraform workspace id` 
**page\_num** |  optional  | Page number of runs returned | numeric | 
**page\_size** |  optional  | Number of runs to return per page \(20 is default\) | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `terraform workspace id` 
action\_result\.parameter\.page\_num | numeric | 
action\_result\.parameter\.page\_size | numeric | 
action\_result\.data\.\*\.meta\.pagination\.prev\-page | string | 
action\_result\.data\.\*\.meta\.pagination\.next\-page | string | 
action\_result\.data\.\*\.meta\.pagination\.current\-page | numeric | 
action\_result\.data\.\*\.meta\.pagination\.total\-pages | numeric | 
action\_result\.data\.\*\.meta\.pagination\.total\-count | numeric | 
action\_result\.data\.\*\.data\.\*\.relationships\.configuration\-version\.data\.type | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.configuration\-version\.data\.id | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.configuration\-version\.links\.related | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.run\-events\.data\.\*\.type | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.run\-events\.data\.\*\.id | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.run\-events\.links\.related | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.comments\.links\.related | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.plan\.data\.type | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.plan\.data\.id | string |  `terraform plan id` 
action\_result\.data\.\*\.data\.\*\.relationships\.plan\.links\.related | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.workspace\.data\.type | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.workspace\.data\.id | string |  `terraform workspace id` 
action\_result\.data\.\*\.data\.\*\.relationships\.apply\.data\.type | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.apply\.data\.id | string |  `terraform apply id` 
action\_result\.data\.\*\.data\.\*\.relationships\.apply\.links\.related | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.policy\-checks\.links\.related | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.created\-by\.data\.type | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.created\-by\.data\.id | string | 
action\_result\.data\.\*\.data\.\*\.relationships\.created\-by\.links\.related | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.status | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.has\-changes | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.canceled\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.created\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.plan\-only | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.actions\.is\-discardable | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.actions\.is\-confirmable | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.actions\.is\-cancelable | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.actions\.is\-force\-cancelable | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.source | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.trigger\-reason | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.status\-timestamps\.planning\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.status\-timestamps\.errored\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.status\-timestamps\.plan\-queued\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.status\-timestamps\.plan\-queueable\-at | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.message | string | 
action\_result\.data\.\*\.data\.\*\.attributes\.is\-destroy | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-force\-execute | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-force\-cancel | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-apply | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-cancel | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-discard | boolean | 
action\_result\.data\.\*\.data\.\*\.attributes\.permissions\.can\-override\-policy\-check | boolean | 
action\_result\.data\.\*\.data\.\*\.type | string | 
action\_result\.data\.\*\.data\.\*\.id | string |  `terraform run id` 
action\_result\.data\.\*\.data\.\*\.links\.self | string | 
action\_result\.data\.\*\.links\.next | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.links\.prev | string | 
action\_result\.data\.\*\.links\.last | string |  `url` 
action\_result\.data\.\*\.links\.first | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create run'
Create a run which will perform a plan and apply

Type: **generic**  
Read only: **False**

NOTE\: This endpoint must be accessed using either a <b>user token</b> or a <b>team token</b>\. A run performs a plan and applies, using a configuration version and the workspace's current variables\. You can specify a configuration version when creating a run; if you don't provide one, the run defaults to the workspace's most recently used version\. \(A configuration version is 'used' when it is created or used for a run in this workspace\.\)\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**workspace\_id** |  required  | ID of workspace where the run will be executed | string |  `terraform workspace id` 
**configuration\_version** |  optional  | Configuration version to use for this run\. If blank, latest config is used | string | 
**message** |  optional  | Message to be associated with this run | string | 
**is\_destroy** |  optional  | Specify if this plan is a destroy plan, which will destroy all provisioned resources | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.configuration\_version | string | 
action\_result\.parameter\.is\_destroy | boolean | 
action\_result\.parameter\.message | string | 
action\_result\.parameter\.workspace\_id | string |  `terraform workspace id` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create workspace'
Create a workspace within Terraform

Type: **generic**  
Read only: **False**

Workspace creation is restricted to members of the owner's team, the owner's team API token, and the organization API token\. The organization must already exist in the system, and the user must have permission to create new workspaces\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**organization\_name** |  required  | Name of the organization to create the workspace within Terraform | string |  `terraform organization name` 
**workspace\_name** |  required  | Name of the workspace | string |  `terraform workspace name` 
**description** |  optional  | Description for the workspace | string | 
**vcs\_repo\_id** |  optional  | Reference to your VSC repo in the format \:org/\:repo | string |  `terraform vcs repo id` 
**vcs\_token\_id** |  optional  | Token ID of the VSC repo | string |  `terraform vcs token id` 
**file\_triggers\_enabled** |  optional  | Whether to filter runs based on the changed files in a VCS push | boolean | 
**auto\_apply** |  optional  | Automatically apply changes when plan is successful | boolean | 
**queue\_all\_runs** |  optional  | Whether runs should be queued immediately after workspace creation | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.organization\_name | string |  `terraform organization name` 
action\_result\.parameter\.workspace\_name | string |  `terraform workspace name` 
action\_result\.parameter\.auto\_apply | boolean | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.file\_triggers\_enabled | string | 
action\_result\.parameter\.queue\_all\_runs | boolean | 
action\_result\.parameter\.vcs\_repo\_id | string |  `terraform vcs repo id` 
action\_result\.parameter\.vcs\_token\_id | string |  `terraform vcs token id` 
action\_result\.data\.\*\.attributes\.actions\.is\-destroyable | boolean | 
action\_result\.data\.\*\.attributes\.auto\-apply | boolean | 
action\_result\.data\.\*\.attributes\.created\-at | string | 
action\_result\.data\.\*\.attributes\.description | string | 
action\_result\.data\.\*\.attributes\.environment | string | 
action\_result\.data\.\*\.attributes\.file\-triggers\-enabled | boolean | 
action\_result\.data\.\*\.attributes\.latest\-change\-at | string | 
action\_result\.data\.\*\.attributes\.locked | boolean | 
action\_result\.data\.\*\.attributes\.name | string |  `terraform workspace name` 
action\_result\.data\.\*\.attributes\.operations | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-destroy | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-force\-unlock | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-lock | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-queue\-apply | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-queue\-destroy | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-queue\-run | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-read\-settings | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-unlock | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-update | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-update\-variable | boolean | 
action\_result\.data\.\*\.attributes\.queue\-all\-runs | boolean | 
action\_result\.data\.\*\.attributes\.source | string | 
action\_result\.data\.\*\.attributes\.source\-name | string | 
action\_result\.data\.\*\.attributes\.source\-url | string | 
action\_result\.data\.\*\.attributes\.speculative\-enabled | boolean | 
action\_result\.data\.\*\.attributes\.terraform\-version | string | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.branch | string | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.identifier | string |  `terraform vcs repo id` 
action\_result\.data\.\*\.attributes\.vcs\-repo\.ingress\-submodules | boolean | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.oauth\-token\-id | string |  `terraform vcs token id` 
action\_result\.data\.\*\.attributes\.working\-directory | string | 
action\_result\.data\.\*\.id | string |  `terraform workspace id` 
action\_result\.data\.\*\.links\.self | string | 
action\_result\.data\.\*\.relationships\.current\-run\.data | string | 
action\_result\.data\.\*\.relationships\.current\-state\-version\.data | string | 
action\_result\.data\.\*\.relationships\.latest\-run\.data | string | 
action\_result\.data\.\*\.relationships\.organization\.data\.id | string | 
action\_result\.data\.\*\.relationships\.organization\.data\.type | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.workspace\_id | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'apply run'
Applies a run that is paused waiting for confirmation after a plan

Type: **generic**  
Read only: **False**

This includes runs in the 'needs confirmation' and 'policy checked' states\. This action is only required for runs that can't be auto\-applied\. \(Plans can be auto\-applied if the auto\-apply setting is enabled on the workspace, the plan is not a destroy plan, and the plan was not queued by a user without write permissions\.\)<br>This endpoint queues the request to perform an apply; the apply might not happen immediately\.<br>This endpoint represents an action as opposed to a resource\. As such, the endpoint does not return any object in the response body\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | The ID of the run to apply | string |  `terraform run id` 
**comment** |  optional  | An optional comment about the run | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `terraform run id` 
action\_result\.parameter\.comment | string | 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get apply'
Get details of an apply

Type: **investigate**  
Read only: **True**

There is no endpoint to list applies\. You can find the ID for an apply in the 'relationships\.apply' property of a run object\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | The ID of the apply to show | string |  `terraform apply id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `terraform apply id` 
action\_result\.data\.\*\.data\.relationships\.state\-versions\.data\.\*\.type | string | 
action\_result\.data\.\*\.data\.relationships\.state\-versions\.data\.\*\.id | string | 
action\_result\.data\.\*\.data\.attributes\.status | string | 
action\_result\.data\.\*\.data\.attributes\.log\-read\-url | string |  `url` 
action\_result\.data\.\*\.data\.attributes\.resource\-changes | numeric | 
action\_result\.data\.\*\.data\.attributes\.resource\-additions | numeric | 
action\_result\.data\.\*\.data\.attributes\.resource\-destructions | numeric | 
action\_result\.data\.\*\.data\.attributes\.status\-timestamps\.queued\-at | string | 
action\_result\.data\.\*\.data\.attributes\.status\-timestamps\.started\-at | string | 
action\_result\.data\.\*\.data\.attributes\.status\-timestamps\.finished\-at | string | 
action\_result\.data\.\*\.data\.type | string | 
action\_result\.data\.\*\.data\.id | string |  `terraform apply id` 
action\_result\.data\.\*\.data\.links\.self | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get plan'
Get details and status of the plan of a run in Terraform

Type: **investigate**  
Read only: **True**

There is no endpoint to list plans\. You can find the ID for a plan in the 'relationships\.plan' property of a run object\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | The ID of the plan to show | string |  `terraform plan id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `terraform plan id` 
action\_result\.data\.\*\.data\.attributes\.status | string | 
action\_result\.data\.\*\.data\.attributes\.has\-changes | boolean | 
action\_result\.data\.\*\.data\.attributes\.log\-read\-url | string |  `url` 
action\_result\.data\.\*\.data\.attributes\.resource\-changes | string | 
action\_result\.data\.\*\.data\.attributes\.actions\.is\-exportable | boolean | 
action\_result\.data\.\*\.data\.attributes\.resource\-additions | string | 
action\_result\.data\.\*\.data\.attributes\.resource\-destructions | string | 
action\_result\.data\.\*\.data\.attributes\.status\-timestamps\.errored\-at | string | 
action\_result\.data\.\*\.data\.attributes\.status\-timestamps\.started\-at | string | 
action\_result\.data\.\*\.data\.attributes\.status\-timestamps\.managed\-queued\-at | string | 
action\_result\.data\.\*\.data\.attributes\.permissions\.can\-export | boolean | 
action\_result\.data\.\*\.data\.type | string | 
action\_result\.data\.\*\.data\.id | string |  `terraform plan id` 
action\_result\.data\.\*\.data\.links\.self | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get run'
This endpoint is used for showing details of a specific run

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | The ID of the run to retrieve details | string |  `terraform run id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `terraform run id` 
action\_result\.data\.\*\.relationships\.configuration\-version\.data\.type | string | 
action\_result\.data\.\*\.relationships\.configuration\-version\.data\.id | string | 
action\_result\.data\.\*\.relationships\.configuration\-version\.links\.related | string | 
action\_result\.data\.\*\.relationships\.run\-events\.data\.\*\.type | string | 
action\_result\.data\.\*\.relationships\.run\-events\.data\.\*\.id | string | 
action\_result\.data\.\*\.relationships\.run\-events\.links\.related | string | 
action\_result\.data\.\*\.relationships\.comments\.links\.related | string | 
action\_result\.data\.\*\.relationships\.plan\.data\.type | string | 
action\_result\.data\.\*\.relationships\.plan\.data\.id | string |  `terraform plan id` 
action\_result\.data\.\*\.relationships\.plan\.links\.related | string | 
action\_result\.data\.\*\.relationships\.workspace\.data\.type | string | 
action\_result\.data\.\*\.relationships\.workspace\.data\.id | string |  `terraform workspace id` 
action\_result\.data\.\*\.relationships\.apply\.data\.type | string | 
action\_result\.data\.\*\.relationships\.apply\.data\.id | string |  `terraform apply id` 
action\_result\.data\.\*\.relationships\.apply\.links\.related | string | 
action\_result\.data\.\*\.relationships\.policy\-checks\.links\.related | string | 
action\_result\.data\.\*\.relationships\.created\-by\.data\.type | string | 
action\_result\.data\.\*\.relationships\.created\-by\.data\.id | string | 
action\_result\.data\.\*\.relationships\.created\-by\.links\.related | string | 
action\_result\.data\.\*\.attributes\.status | string | 
action\_result\.data\.\*\.attributes\.has\-changes | boolean | 
action\_result\.data\.\*\.attributes\.canceled\-at | string | 
action\_result\.data\.\*\.attributes\.created\-at | string | 
action\_result\.data\.\*\.attributes\.plan\-only | boolean | 
action\_result\.data\.\*\.attributes\.actions\.is\-discardable | boolean | 
action\_result\.data\.\*\.attributes\.actions\.is\-confirmable | boolean | 
action\_result\.data\.\*\.attributes\.actions\.is\-cancelable | boolean | 
action\_result\.data\.\*\.attributes\.actions\.is\-force\-cancelable | boolean | 
action\_result\.data\.\*\.attributes\.source | string | 
action\_result\.data\.\*\.attributes\.trigger\-reason | string | 
action\_result\.data\.\*\.attributes\.status\-timestamps\.planning\-at | string | 
action\_result\.data\.\*\.attributes\.status\-timestamps\.errored\-at | string | 
action\_result\.data\.\*\.attributes\.status\-timestamps\.plan\-queued\-at | string | 
action\_result\.data\.\*\.attributes\.status\-timestamps\.plan\-queueable\-at | string | 
action\_result\.data\.\*\.attributes\.message | string | 
action\_result\.data\.\*\.attributes\.is\-destroy | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-force\-execute | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-force\-cancel | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-apply | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-cancel | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-discard | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-override\-policy\-check | boolean | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.id | string |  `terraform run id` 
action\_result\.data\.\*\.links\.self | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get workspace'
Get details of a workspace

Type: **investigate**  
Read only: **True**

Details on a workspace can be retrieved from two endpoints, which behave identically\. One refers to a workspace by its ID, and the other by its name and organization\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  optional  | The ID of the workspace to show | string |  `terraform workspace id` 
**organization\_name** |  optional  | The name of the organization to retrieve workspace details | string |  `terraform organization name` 
**workspace\_name** |  optional  | The name of the workspace to retrieve details | string |  `terraform workspace name` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `terraform workspace id` 
action\_result\.parameter\.organization\_name | string |  `terraform organization name` 
action\_result\.parameter\.workspace\_name | string |  `terraform workspace name` 
action\_result\.data\.\*\.relationships\.organization\.data\.type | string | 
action\_result\.data\.\*\.relationships\.organization\.data\.id | string |  `terraform organization name` 
action\_result\.data\.\*\.relationships\.latest\-run\.data\.type | string | 
action\_result\.data\.\*\.relationships\.latest\-run\.data\.id | string |  `terraform run id` 
action\_result\.data\.\*\.relationships\.latest\-run\.links\.related | string | 
action\_result\.data\.\*\.relationships\.current\-run\.data\.type | string | 
action\_result\.data\.\*\.relationships\.current\-run\.data\.id | string |  `terraform run id` 
action\_result\.data\.\*\.relationships\.current\-run\.links\.related | string | 
action\_result\.data\.\*\.relationships\.current\-state\-version\.data | string | 
action\_result\.data\.\*\.attributes\.operations | boolean | 
action\_result\.data\.\*\.attributes\.environment | string | 
action\_result\.data\.\*\.attributes\.source\-name | string | 
action\_result\.data\.\*\.attributes\.locked | boolean | 
action\_result\.data\.\*\.attributes\.name | string |  `terraform workspace name` 
action\_result\.data\.\*\.attributes\.auto\-apply | boolean | 
action\_result\.data\.\*\.attributes\.terraform\-version | string | 
action\_result\.data\.\*\.attributes\.description | string | 
action\_result\.data\.\*\.attributes\.created\-at | string | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.display\-identifier | string | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.identifier | string | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.github\-app\-installation\-id | string | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.ingress\-submodules | boolean | 
action\_result\.data\.\*\.attributes\.vcs\-repo\.branch | string | 
action\_result\.data\.\*\.attributes\.actions\.is\-destroyable | boolean | 
action\_result\.data\.\*\.attributes\.queue\-all\-runs | boolean | 
action\_result\.data\.\*\.attributes\.source | string | 
action\_result\.data\.\*\.attributes\.latest\-change\-at | string | 
action\_result\.data\.\*\.attributes\.source\-url | string | 
action\_result\.data\.\*\.attributes\.working\-directory | string | 
action\_result\.data\.\*\.attributes\.vcs\-repo\-identifier | string | 
action\_result\.data\.\*\.attributes\.file\-triggers\-enabled | boolean | 
action\_result\.data\.\*\.attributes\.speculative\-enabled | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-destroy | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-lock | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-force\-unlock | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-queue\-apply | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-queue\-run | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-read\-settings | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-unlock | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-update\-variable | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-queue\-destroy | boolean | 
action\_result\.data\.\*\.attributes\.permissions\.can\-update | boolean | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.id | string |  `terraform workspace id` 
action\_result\.data\.\*\.links\.self | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 