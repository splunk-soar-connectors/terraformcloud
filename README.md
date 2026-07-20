# Terraform Cloud

Publisher: Splunk Community <br>
Connector Version: 1.0.10 <br>
Product Vendor: HashiCorp <br>
Product Name: Terraform Cloud <br>
Minimum Product Version: 4.8.24304

This app integrates with Terraform Cloud to perform generic and investigative actions to manage runs, plans, and applies

### Configuration variables

This table lists the configuration variables required to operate Terraform Cloud. These variables are specified when configuring a Terraform Cloud asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base_url** | optional | string | Terraform URL (e.g. https://app.terraform.io) |
**verify_server_cert** | optional | boolean | Verify server SSL certificate |
**token** | required | password | Authentication Token |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration <br>
[list workspaces](#action-list-workspaces) - Lists workspaces in the organization <br>
[list runs](#action-list-runs) - Lists runs for a workspace <br>
[create run](#action-create-run) - Create a run which will perform a plan and apply <br>
[create workspace](#action-create-workspace) - Create a workspace within Terraform <br>
[apply run](#action-apply-run) - Applies a run that is paused waiting for confirmation after a plan <br>
[get apply](#action-get-apply) - Get details of an apply <br>
[get plan](#action-get-plan) - Get details and status of the plan of a run in Terraform <br>
[get run](#action-get-run) - This endpoint is used for showing details of a specific run <br>
[get workspace](#action-get-workspace) - Get details of a workspace

## action: 'test connectivity'

Validate the asset configuration for connectivity using supplied configuration

Type: **test** <br>
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'list workspaces'

Lists workspaces in the organization

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**organization_name** | required | Name of the organization to list the workspaces of | string | `terraform organization name` |
**page_num** | optional | Page number of workspace list | numeric | |
**page_size** | optional | Number of workspaces to return per page (100 is default) | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.organization_name | string | `terraform organization name` | Organization |
action_result.parameter.page_num | numeric | | |
action_result.parameter.page_size | numeric | | |
action_result.data.\*.meta.pagination.prev-page | string | | |
action_result.data.\*.meta.pagination.next-page | string | | |
action_result.data.\*.meta.pagination.current-page | numeric | | 1 |
action_result.data.\*.meta.pagination.total-pages | numeric | | 1 |
action_result.data.\*.meta.pagination.total-count | numeric | | 1 |
action_result.data.\*.meta.status-counts.applied | numeric | | 0 |
action_result.data.\*.meta.status-counts.discarded | numeric | | 0 |
action_result.data.\*.meta.status-counts.none | numeric | | 1 |
action_result.data.\*.meta.status-counts.applying | numeric | | 0 |
action_result.data.\*.meta.status-counts.cost-estimated | numeric | | 0 |
action_result.data.\*.meta.status-counts.plan-queued | numeric | | 0 |
action_result.data.\*.meta.status-counts.policy-checked | numeric | | 0 |
action_result.data.\*.meta.status-counts.cost-estimating | numeric | | 0 |
action_result.data.\*.meta.status-counts.confirmed | numeric | | 0 |
action_result.data.\*.meta.status-counts.policy-soft-failed | numeric | | 0 |
action_result.data.\*.meta.status-counts.policy-override | numeric | | 0 |
action_result.data.\*.meta.status-counts.canceled | numeric | | 0 |
action_result.data.\*.meta.status-counts.apply-queued | numeric | | 0 |
action_result.data.\*.meta.status-counts.planning | numeric | | 0 |
action_result.data.\*.meta.status-counts.planned | numeric | | 0 |
action_result.data.\*.meta.status-counts.policy-checking | numeric | | 0 |
action_result.data.\*.meta.status-counts.errored | numeric | | 0 |
action_result.data.\*.meta.status-counts.total | numeric | | 1 |
action_result.data.\*.meta.status-counts.pending | numeric | | 0 |
action_result.data.\*.meta.status-counts.planned-and-finished | numeric | | 0 |
action_result.data.\*.data.\*.relationships.organization.data.type | string | | organizations |
action_result.data.\*.data.\*.relationships.organization.data.id | string | `terraform organization name` | Organization |
action_result.data.\*.data.\*.relationships.latest-run.data | string | | |
action_result.data.\*.data.\*.relationships.current-run.data | string | | |
action_result.data.\*.data.\*.relationships.current-state-version.data | string | | |
action_result.data.\*.data.\*.attributes.operations | boolean | | True False |
action_result.data.\*.data.\*.attributes.environment | string | | default |
action_result.data.\*.data.\*.attributes.source-name | string | | |
action_result.data.\*.data.\*.attributes.locked | boolean | | True False |
action_result.data.\*.data.\*.attributes.name | string | `terraform workspace name` | test_workspace |
action_result.data.\*.data.\*.attributes.auto-apply | boolean | | True False |
action_result.data.\*.data.\*.attributes.terraform-version | string | | 0.12.18 |
action_result.data.\*.data.\*.attributes.description | string | | This is a test description |
action_result.data.\*.data.\*.attributes.created-at | string | | 2019-12-20T19:31:36.463Z |
action_result.data.\*.data.\*.attributes.vcs-repo | string | | |
action_result.data.\*.data.\*.attributes.actions.is-destroyable | boolean | | True False |
action_result.data.\*.data.\*.attributes.queue-all-runs | boolean | | True False |
action_result.data.\*.data.\*.attributes.source | string | | tfe-api |
action_result.data.\*.data.\*.attributes.latest-change-at | string | | 2019-12-20T19:31:36.463Z |
action_result.data.\*.data.\*.attributes.working-directory | string | | |
action_result.data.\*.data.\*.attributes.source-url | string | | |
action_result.data.\*.data.\*.attributes.file-triggers-enabled | boolean | | True False |
action_result.data.\*.data.\*.attributes.speculative-enabled | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-destroy | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-lock | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-force-unlock | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-queue-apply | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-queue-run | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-read-settings | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-unlock | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-update-variable | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-queue-destroy | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-update | boolean | | True False |
action_result.data.\*.data.\*.type | string | | workspaces |
action_result.data.\*.data.\*.id | string | `terraform workspace id` | ws-X9wL9pBZQdE6gjsp |
action_result.data.\*.data.\*.links.self | string | | /api/v2/organizations/TestOrg/workspaces/test_workspace |
action_result.data.\*.links.next | string | | |
action_result.data.\*.links.self | string | `url` | https://app.terraform.io/api/v2/organizations/TestOrg/workspaces?page%5Bnumber%5D=1&page%5Bsize%5D=100 |
action_result.data.\*.links.prev | string | | |
action_result.data.\*.links.last | string | `url` | https://app.terraform.io/api/v2/organizations/TestOrg/workspaces?page%5Bnumber%5D=1&page%5Bsize%5D=100 |
action_result.data.\*.links.first | string | `url` | https://app.terraform.io/api/v2/organizations/TestOrg/workspaces?page%5Bnumber%5D=1&page%5Bsize%5D=100 |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list runs'

Lists runs for a workspace

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Name of the organization to list the workspaces of | string | `terraform workspace id` |
**page_num** | optional | Page number of runs returned | numeric | |
**page_size** | optional | Number of runs to return per page (20 is default) | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.id | string | `terraform workspace id` | ws-X9wL9pBZQdE6gjsp |
action_result.parameter.page_num | numeric | | |
action_result.parameter.page_size | numeric | | |
action_result.data.\*.meta.pagination.prev-page | string | | |
action_result.data.\*.meta.pagination.next-page | string | | |
action_result.data.\*.meta.pagination.current-page | numeric | | 1 |
action_result.data.\*.meta.pagination.total-pages | numeric | | 1 |
action_result.data.\*.meta.pagination.total-count | numeric | | 1 |
action_result.data.\*.data.\*.relationships.configuration-version.data.type | string | | configuration-versions |
action_result.data.\*.data.\*.relationships.configuration-version.data.id | string | | cv-ybgt5G3jpbW72V1s |
action_result.data.\*.data.\*.relationships.configuration-version.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/configuration-version |
action_result.data.\*.data.\*.relationships.run-events.data.\*.type | string | | run-events |
action_result.data.\*.data.\*.relationships.run-events.data.\*.id | string | | re-y9FL2wcGKNsUdG2a |
action_result.data.\*.data.\*.relationships.run-events.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/run-events |
action_result.data.\*.data.\*.relationships.comments.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/comments |
action_result.data.\*.data.\*.relationships.plan.data.type | string | | plans |
action_result.data.\*.data.\*.relationships.plan.data.id | string | `terraform plan id` | plan-iB6dV91zqE5pNCey |
action_result.data.\*.data.\*.relationships.plan.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/plan |
action_result.data.\*.data.\*.relationships.workspace.data.type | string | | workspaces |
action_result.data.\*.data.\*.relationships.workspace.data.id | string | `terraform workspace id` | ws-X9wL9pBZQdE6gjsp |
action_result.data.\*.data.\*.relationships.apply.data.type | string | | applies |
action_result.data.\*.data.\*.relationships.apply.data.id | string | `terraform apply id` | apply-eK21impkqMUvxZTw |
action_result.data.\*.data.\*.relationships.apply.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/apply |
action_result.data.\*.data.\*.relationships.policy-checks.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/policy-checks |
action_result.data.\*.data.\*.relationships.created-by.data.type | string | | users |
action_result.data.\*.data.\*.relationships.created-by.data.id | string | | user-NU2TLU1zsmvguG3K |
action_result.data.\*.data.\*.relationships.created-by.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/created-by |
action_result.data.\*.data.\*.attributes.status | string | | errored |
action_result.data.\*.data.\*.attributes.has-changes | boolean | | True False |
action_result.data.\*.data.\*.attributes.canceled-at | string | | |
action_result.data.\*.data.\*.attributes.created-at | string | | 2020-01-08T21:25:53.076Z |
action_result.data.\*.data.\*.attributes.plan-only | boolean | | True False |
action_result.data.\*.data.\*.attributes.actions.is-discardable | boolean | | True False |
action_result.data.\*.data.\*.attributes.actions.is-confirmable | boolean | | True False |
action_result.data.\*.data.\*.attributes.actions.is-cancelable | boolean | | True False |
action_result.data.\*.data.\*.attributes.actions.is-force-cancelable | boolean | | True False |
action_result.data.\*.data.\*.attributes.source | string | | tfe-ui |
action_result.data.\*.data.\*.attributes.trigger-reason | string | | manual |
action_result.data.\*.data.\*.attributes.status-timestamps.planning-at | string | | 2020-01-08T21:25:53+00:00 |
action_result.data.\*.data.\*.attributes.status-timestamps.errored-at | string | | 2020-01-08T21:26:00+00:00 |
action_result.data.\*.data.\*.attributes.status-timestamps.plan-queued-at | string | | 2020-01-08T21:25:53+00:00 |
action_result.data.\*.data.\*.attributes.status-timestamps.plan-queueable-at | string | | 2020-01-08T21:25:53+00:00 |
action_result.data.\*.data.\*.attributes.message | string | | Queued from Terraform Cloud UI |
action_result.data.\*.data.\*.attributes.is-destroy | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-force-execute | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-force-cancel | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-apply | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-cancel | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-discard | boolean | | True False |
action_result.data.\*.data.\*.attributes.permissions.can-override-policy-check | boolean | | True False |
action_result.data.\*.data.\*.type | string | | runs |
action_result.data.\*.data.\*.id | string | `terraform run id` | run-B45D8uRipKCtvpYd |
action_result.data.\*.data.\*.links.self | string | | /api/v2/runs/run-B45D8uRipKCtvpYd |
action_result.data.\*.links.next | string | | |
action_result.data.\*.links.self | string | `url` | https://app.terraform.io/api/v2/workspaces/ws-X9wL9pBZQdE6gjsp/runs?page%5Bnumber%5D=1&page%5Bsize%5D=20 |
action_result.data.\*.links.prev | string | | |
action_result.data.\*.links.last | string | `url` | https://app.terraform.io/api/v2/workspaces/ws-X9wL9pBZQdE6gjsp/runs?page%5Bnumber%5D=1&page%5Bsize%5D=20 |
action_result.data.\*.links.first | string | `url` | https://app.terraform.io/api/v2/workspaces/ws-X9wL9pBZQdE6gjsp/runs?page%5Bnumber%5D=1&page%5Bsize%5D=20 |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create run'

Create a run which will perform a plan and apply

Type: **generic** <br>
Read only: **False**

NOTE: This endpoint must be accessed using either a <b>user token</b> or a <b>team token</b>. A run performs a plan and applies, using a configuration version and the workspace's current variables. You can specify a configuration version when creating a run; if you don't provide one, the run defaults to the workspace's most recently used version. (A configuration version is 'used' when it is created or used for a run in this workspace.).

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**workspace_id** | required | ID of workspace where the run will be executed | string | `terraform workspace id` |
**configuration_version** | optional | Configuration version to use for this run. If blank, latest config is used | string | |
**message** | optional | Message to be associated with this run | string | |
**is_destroy** | optional | Specify if this plan is a destroy plan, which will destroy all provisioned resources | boolean | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.configuration_version | string | | |
action_result.parameter.is_destroy | boolean | | True False |
action_result.parameter.message | string | | |
action_result.parameter.workspace_id | string | `terraform workspace id` | |
action_result.data | string | | |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create workspace'

Create a workspace within Terraform

Type: **generic** <br>
Read only: **False**

Workspace creation is restricted to members of the owner's team, the owner's team API token, and the organization API token. The organization must already exist in the system, and the user must have permission to create new workspaces.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**organization_name** | required | Name of the organization to create the workspace within Terraform | string | `terraform organization name` |
**workspace_name** | required | Name of the workspace | string | `terraform workspace name` |
**description** | optional | Description for the workspace | string | |
**vcs_repo_id** | optional | Reference to your VSC repo in the format :org/:repo | string | `terraform vcs repo id` |
**vcs_token_id** | optional | Token ID of the VSC repo | string | `terraform vcs token id` |
**file_triggers_enabled** | optional | Whether to filter runs based on the changed files in a VCS push | boolean | |
**auto_apply** | optional | Automatically apply changes when plan is successful | boolean | |
**queue_all_runs** | optional | Whether runs should be queued immediately after workspace creation | boolean | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.organization_name | string | `terraform organization name` | TestOrg |
action_result.parameter.workspace_name | string | `terraform workspace name` | test_workspace |
action_result.parameter.auto_apply | boolean | | True False |
action_result.parameter.description | string | | This is a test description |
action_result.parameter.file_triggers_enabled | string | | true |
action_result.parameter.queue_all_runs | boolean | | True False |
action_result.parameter.vcs_repo_id | string | `terraform vcs repo id` | |
action_result.parameter.vcs_token_id | string | `terraform vcs token id` | |
action_result.data.\*.attributes.actions.is-destroyable | boolean | | True False |
action_result.data.\*.attributes.auto-apply | boolean | | True False |
action_result.data.\*.attributes.created-at | string | | 2019-12-20T19:31:36.463Z |
action_result.data.\*.attributes.description | string | | This is a test description |
action_result.data.\*.attributes.environment | string | | default |
action_result.data.\*.attributes.file-triggers-enabled | boolean | | True False |
action_result.data.\*.attributes.latest-change-at | string | | 2019-12-20T19:31:36.463Z |
action_result.data.\*.attributes.locked | boolean | | True False |
action_result.data.\*.attributes.name | string | `terraform workspace name` | test_workspace |
action_result.data.\*.attributes.operations | boolean | | True False |
action_result.data.\*.attributes.permissions.can-destroy | boolean | | True False |
action_result.data.\*.attributes.permissions.can-force-unlock | boolean | | True False |
action_result.data.\*.attributes.permissions.can-lock | boolean | | True False |
action_result.data.\*.attributes.permissions.can-queue-apply | boolean | | True False |
action_result.data.\*.attributes.permissions.can-queue-destroy | boolean | | True False |
action_result.data.\*.attributes.permissions.can-queue-run | boolean | | True False |
action_result.data.\*.attributes.permissions.can-read-settings | boolean | | True False |
action_result.data.\*.attributes.permissions.can-unlock | boolean | | True False |
action_result.data.\*.attributes.permissions.can-update | boolean | | True False |
action_result.data.\*.attributes.permissions.can-update-variable | boolean | | True False |
action_result.data.\*.attributes.queue-all-runs | boolean | | True False |
action_result.data.\*.attributes.source | string | | tfe-api |
action_result.data.\*.attributes.source-name | string | | |
action_result.data.\*.attributes.source-url | string | | |
action_result.data.\*.attributes.speculative-enabled | boolean | | True False |
action_result.data.\*.attributes.terraform-version | string | | 0.12.18 |
action_result.data.\*.attributes.vcs-repo.branch | string | | |
action_result.data.\*.attributes.vcs-repo.identifier | string | `terraform vcs repo id` | |
action_result.data.\*.attributes.vcs-repo.ingress-submodules | boolean | | True False |
action_result.data.\*.attributes.vcs-repo.oauth-token-id | string | `terraform vcs token id` | |
action_result.data.\*.attributes.working-directory | string | | |
action_result.data.\*.id | string | `terraform workspace id` | ws-1jIskLtjsp |
action_result.data.\*.links.self | string | | /api/v2/organizations/TestOrg/workspaces/test_workspace |
action_result.data.\*.relationships.current-run.data | string | | |
action_result.data.\*.relationships.current-state-version.data | string | | |
action_result.data.\*.relationships.latest-run.data | string | | |
action_result.data.\*.relationships.organization.data.id | string | | TestOrg |
action_result.data.\*.relationships.organization.data.type | string | | organizations |
action_result.data.\*.type | string | | workspaces |
action_result.status | string | | success failed |
action_result.message | string | | Workspace id: ws-1jIskLtjsp |
action_result.summary.workspace_id | string | | ws-1jIskLtjsp |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |
action_result.parameter.ph_0 | ph | | |

## action: 'apply run'

Applies a run that is paused waiting for confirmation after a plan

Type: **generic** <br>
Read only: **False**

This includes runs in the 'needs confirmation' and 'policy checked' states. This action is only required for runs that can't be auto-applied. (Plans can be auto-applied if the auto-apply setting is enabled on the workspace, the plan is not a destroy plan, and the plan was not queued by a user without write permissions.)<br>This endpoint queues the request to perform an apply; the apply might not happen immediately.<br>This endpoint represents an action as opposed to a resource. As such, the endpoint does not return any object in the response body.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | The ID of the run to apply | string | `terraform run id` |
**comment** | optional | An optional comment about the run | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.id | string | `terraform run id` | |
action_result.parameter.comment | string | | |
action_result.data | string | | |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get apply'

Get details of an apply

Type: **investigate** <br>
Read only: **True**

There is no endpoint to list applies. You can find the ID for an apply in the 'relationships.apply' property of a run object.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | The ID of the apply to show | string | `terraform apply id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.id | string | `terraform apply id` | apply-Kasd12SWa9AhS6 |
action_result.data.\*.data.relationships.state-versions.data.\*.type | string | | state-versions |
action_result.data.\*.data.relationships.state-versions.data.\*.id | string | | sv-23dawhGdsaoMG |
action_result.data.\*.data.attributes.status | string | | finished |
action_result.data.\*.data.attributes.log-read-url | string | `url` | https://terraform.com/v1/object/0dWMmnMUFkQjRu |
action_result.data.\*.data.attributes.resource-changes | numeric | | 0 |
action_result.data.\*.data.attributes.resource-additions | numeric | | 1 |
action_result.data.\*.data.attributes.resource-destructions | numeric | | 0 |
action_result.data.\*.data.attributes.status-timestamps.queued-at | string | | 2019-11-13T21:53:45+00:00 |
action_result.data.\*.data.attributes.status-timestamps.started-at | string | | 2019-11-13T21:53:47+00:00 |
action_result.data.\*.data.attributes.status-timestamps.finished-at | string | | 2019-11-13T21:54:16+00:00 |
action_result.data.\*.data.type | string | | applies |
action_result.data.\*.data.id | string | `terraform apply id` | apply-Kasd12SWa9AhS6 |
action_result.data.\*.data.links.self | string | | /api/v2/applies/apply-Kasd12SWa9AhS6 |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get plan'

Get details and status of the plan of a run in Terraform

Type: **investigate** <br>
Read only: **True**

There is no endpoint to list plans. You can find the ID for a plan in the 'relationships.plan' property of a run object.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | The ID of the plan to show | string | `terraform plan id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.id | string | `terraform plan id` | plan-iB6dV91zqE5pNCey |
action_result.data.\*.data.attributes.status | string | | errored |
action_result.data.\*.data.attributes.has-changes | boolean | | True False |
action_result.data.\*.data.attributes.log-read-url | string | `url` | https://archivist.terraform.io/v1/object/dmF1bHQ6djE6RFk0YlNjcUg1T1IrN3ptUEpIeXJyM0pZaHpqL09MVlY5bkREWVljeU8xeEJCR2FLVDFwdUpHMU9KT0hRZ2FSMy9uaytGRWRMUHdhemtCVWdwbEtBVXpRYVZyOU1XcVRJcnF3bVlVUUZDbHhPRHEvZEdvR2pZK2kzdWtIaWVNZE1aWmdhY0FTVUppR1ZoaU9FeHR0YjJpdnFKSHN5aUFsM2dvVzJ5YzJVMEhway9lQU13VHFySWlhS0hRRUpHL0ZENUVlRjFWUERVQWpSRXJWYmNKalRZWEhOT0VZeGplbUFJbk5KL2tPcmJZSnNzRHVGaHZPVHZpSjVsMGFnaFBhZXg4ZFN2MzF4R1YwY3JiejZaWGRhU1gyVDlmaXRySStkVS9pNnJUTzBOV1BVbkI4U0FoTUpxYU5sZ0VWQUV3emNHTHdybnNycHJxRkRlcmx5dXlTQkhzWlRhMnF0Q0xhLzlJMnV5M25Xc0EvZ0RrK3ZheU5DVWhnNk9oQT0 |
action_result.data.\*.data.attributes.resource-changes | string | | |
action_result.data.\*.data.attributes.actions.is-exportable | boolean | | True False |
action_result.data.\*.data.attributes.resource-additions | string | | |
action_result.data.\*.data.attributes.resource-destructions | string | | |
action_result.data.\*.data.attributes.status-timestamps.errored-at | string | | 2020-01-08T21:26:00+00:00 |
action_result.data.\*.data.attributes.status-timestamps.started-at | string | | 2020-01-08T21:25:54+00:00 |
action_result.data.\*.data.attributes.status-timestamps.managed-queued-at | string | | 2020-01-08T21:25:53+00:00 |
action_result.data.\*.data.attributes.permissions.can-export | boolean | | True False |
action_result.data.\*.data.type | string | | plans |
action_result.data.\*.data.id | string | `terraform plan id` | plan-iB6dV91zqE5pNCey |
action_result.data.\*.data.links.self | string | | /api/v2/plans/plan-iB6dV91zqE5pNCey |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get run'

This endpoint is used for showing details of a specific run

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | The ID of the run to retrieve details | string | `terraform run id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.id | string | `terraform run id` | run-B45D8uRipKCtvpYd |
action_result.data.\*.relationships.configuration-version.data.type | string | | configuration-versions |
action_result.data.\*.relationships.configuration-version.data.id | string | | cv-ybgt5G3jpbW72V1s |
action_result.data.\*.relationships.configuration-version.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/configuration-version |
action_result.data.\*.relationships.run-events.data.\*.type | string | | run-events |
action_result.data.\*.relationships.run-events.data.\*.id | string | | re-y9FL2wcGKNsUdG2a |
action_result.data.\*.relationships.run-events.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/run-events |
action_result.data.\*.relationships.comments.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/comments |
action_result.data.\*.relationships.plan.data.type | string | | plans |
action_result.data.\*.relationships.plan.data.id | string | `terraform plan id` | plan-iB6dV91zqE5pNCey |
action_result.data.\*.relationships.plan.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/plan |
action_result.data.\*.relationships.workspace.data.type | string | | workspaces |
action_result.data.\*.relationships.workspace.data.id | string | `terraform workspace id` | ws-X9wL9pBZQdE6gjsp |
action_result.data.\*.relationships.apply.data.type | string | | applies |
action_result.data.\*.relationships.apply.data.id | string | `terraform apply id` | apply-eK21impkqMUvxZTw |
action_result.data.\*.relationships.apply.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/apply |
action_result.data.\*.relationships.policy-checks.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/policy-checks |
action_result.data.\*.relationships.created-by.data.type | string | | users |
action_result.data.\*.relationships.created-by.data.id | string | | user-NU2TLU1zsmvguG3K |
action_result.data.\*.relationships.created-by.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd/created-by |
action_result.data.\*.attributes.status | string | | errored |
action_result.data.\*.attributes.has-changes | boolean | | True False |
action_result.data.\*.attributes.canceled-at | string | | |
action_result.data.\*.attributes.created-at | string | | 2020-01-08T21:25:53.076Z |
action_result.data.\*.attributes.plan-only | boolean | | True False |
action_result.data.\*.attributes.actions.is-discardable | boolean | | True False |
action_result.data.\*.attributes.actions.is-confirmable | boolean | | True False |
action_result.data.\*.attributes.actions.is-cancelable | boolean | | True False |
action_result.data.\*.attributes.actions.is-force-cancelable | boolean | | True False |
action_result.data.\*.attributes.source | string | | tfe-ui |
action_result.data.\*.attributes.trigger-reason | string | | manual |
action_result.data.\*.attributes.status-timestamps.planning-at | string | | 2020-01-08T21:25:53+00:00 |
action_result.data.\*.attributes.status-timestamps.errored-at | string | | 2020-01-08T21:26:00+00:00 |
action_result.data.\*.attributes.status-timestamps.plan-queued-at | string | | 2020-01-08T21:25:53+00:00 |
action_result.data.\*.attributes.status-timestamps.plan-queueable-at | string | | 2020-01-08T21:25:53+00:00 |
action_result.data.\*.attributes.message | string | | Queued from Terraform Cloud UI |
action_result.data.\*.attributes.is-destroy | boolean | | True False |
action_result.data.\*.attributes.permissions.can-force-execute | boolean | | True False |
action_result.data.\*.attributes.permissions.can-force-cancel | boolean | | True False |
action_result.data.\*.attributes.permissions.can-apply | boolean | | True False |
action_result.data.\*.attributes.permissions.can-cancel | boolean | | True False |
action_result.data.\*.attributes.permissions.can-discard | boolean | | True False |
action_result.data.\*.attributes.permissions.can-override-policy-check | boolean | | True False |
action_result.data.\*.type | string | | runs |
action_result.data.\*.id | string | `terraform run id` | run-B45D8uRipKCtvpYd |
action_result.data.\*.links.self | string | | /api/v2/runs/run-B45D8uRipKCtvpYd |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get workspace'

Get details of a workspace

Type: **investigate** <br>
Read only: **True**

Details on a workspace can be retrieved from two endpoints, which behave identically. One refers to a workspace by its ID, and the other by its name and organization.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | optional | The ID of the workspace to show | string | `terraform workspace id` |
**organization_name** | optional | The name of the organization to retrieve workspace details | string | `terraform organization name` |
**workspace_name** | optional | The name of the workspace to retrieve details | string | `terraform workspace name` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.id | string | `terraform workspace id` | |
action_result.parameter.organization_name | string | `terraform organization name` | Organization |
action_result.parameter.workspace_name | string | `terraform workspace name` | test_workspace |
action_result.data.\*.relationships.organization.data.type | string | | organizations |
action_result.data.\*.relationships.organization.data.id | string | `terraform organization name` | Organization |
action_result.data.\*.relationships.latest-run.data.type | string | | runs |
action_result.data.\*.relationships.latest-run.data.id | string | `terraform run id` | run-B45D8uRipKCtvpYd |
action_result.data.\*.relationships.latest-run.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd |
action_result.data.\*.relationships.current-run.data.type | string | | runs |
action_result.data.\*.relationships.current-run.data.id | string | `terraform run id` | run-B45D8uRipKCtvpYd |
action_result.data.\*.relationships.current-run.links.related | string | | /api/v2/runs/run-B45D8uRipKCtvpYd |
action_result.data.\*.relationships.current-state-version.data | string | | |
action_result.data.\*.attributes.operations | boolean | | True False |
action_result.data.\*.attributes.environment | string | | default |
action_result.data.\*.attributes.source-name | string | | |
action_result.data.\*.attributes.locked | boolean | | True False |
action_result.data.\*.attributes.name | string | `terraform workspace name` | test_workspace |
action_result.data.\*.attributes.auto-apply | boolean | | True False |
action_result.data.\*.attributes.terraform-version | string | | 0.12.18 |
action_result.data.\*.attributes.description | string | | This is a test description |
action_result.data.\*.attributes.created-at | string | | 2019-12-20T19:31:36.463Z |
action_result.data.\*.attributes.vcs-repo.display-identifier | string | | jdoe/TestingAPI |
action_result.data.\*.attributes.vcs-repo.identifier | string | | jdoe/TestingAPI |
action_result.data.\*.attributes.vcs-repo.github-app-installation-id | string | | ghain-Mrjk7oxpsgekbwqf |
action_result.data.\*.attributes.vcs-repo.ingress-submodules | boolean | | True False |
action_result.data.\*.attributes.vcs-repo.branch | string | | |
action_result.data.\*.attributes.actions.is-destroyable | boolean | | True False |
action_result.data.\*.attributes.queue-all-runs | boolean | | True False |
action_result.data.\*.attributes.source | string | | tfe-api |
action_result.data.\*.attributes.latest-change-at | string | | 2019-12-20T19:31:36.463Z |
action_result.data.\*.attributes.source-url | string | | |
action_result.data.\*.attributes.working-directory | string | | |
action_result.data.\*.attributes.vcs-repo-identifier | string | | jdoe/TestingAPI |
action_result.data.\*.attributes.file-triggers-enabled | boolean | | True False |
action_result.data.\*.attributes.speculative-enabled | boolean | | True False |
action_result.data.\*.attributes.permissions.can-destroy | boolean | | True False |
action_result.data.\*.attributes.permissions.can-lock | boolean | | True False |
action_result.data.\*.attributes.permissions.can-force-unlock | boolean | | True False |
action_result.data.\*.attributes.permissions.can-queue-apply | boolean | | True False |
action_result.data.\*.attributes.permissions.can-queue-run | boolean | | True False |
action_result.data.\*.attributes.permissions.can-read-settings | boolean | | True False |
action_result.data.\*.attributes.permissions.can-unlock | boolean | | True False |
action_result.data.\*.attributes.permissions.can-update-variable | boolean | | True False |
action_result.data.\*.attributes.permissions.can-queue-destroy | boolean | | True False |
action_result.data.\*.attributes.permissions.can-update | boolean | | True False |
action_result.data.\*.type | string | | workspaces |
action_result.data.\*.id | string | `terraform workspace id` | ws-X9wL9pBZQdE6gjsp |
action_result.data.\*.links.self | string | | /api/v2/organizations/TestOrg/workspaces/test_workspace |
action_result.status | string | | success failed |
action_result.message | string | | |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2026 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
