# Can I modify default checks?

SQLWATCH comes with a set of pre-defined default checks that ensure health of the core components. They are very lightweith queries that will not impact performance in any way and is best to leave them untouched. Default checks negative `check_id` values and user checks have positive values. Every new release of SQLWATCH may add new checks or improve existing checks.

However, when user modifies a default check, the changes will never be overwritten by subsequent SQLWATCH deployments. This is done by design as you know your SQL Instance best and if you make a decision that default checks do not work for you, we will respect that.

