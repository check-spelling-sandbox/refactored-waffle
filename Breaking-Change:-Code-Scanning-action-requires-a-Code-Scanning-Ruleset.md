# Code Scanning action requires a Code Scanning Ruleset

As of [check-spelling v0.0.25](https://github.com/check-spelling/check-spelling/releases/tag/v0.0.25), if you enable [SARIF output](./Feature:-SARIF-output.md), then check-spelling will not yield an :x: for errors. If you are relying on status checks, you'll need to add a code-scanning rule instead. The following is an example of a code-scanning rule which should work:

## Sample ruleset

```json
{
  "name": "check-spelling",
  "target": "branch",
  "source_type": "Repository",
  "enforcement": "active",
  "conditions": {
    "ref_name": {
      "exclude": [],
      "include": [
        "~DEFAULT_BRANCH",
        "refs/heads/master",
        "refs/heads/main"
      ]
    }
  },
  "rules": [
    {
      "type": "deletion"
    },
    {
      "type": "non_fast_forward"
    },
    {
      "type": "required_linear_history"
    },
    {
      "type": "code_scanning",
      "parameters": {
        "code_scanning_tools": [
          {
            "tool": "check-spelling",
            "security_alerts_threshold": "high_or_higher",
            "alerts_threshold": "errors"
          }
        ]
      }
    }
  ],
  "bypass_actors": []
}
```

## Information about Rulesets

For more information on Rulesets, see [Creating rulesets for a repository](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/creating-rulesets-for-a-repository).

---
[FAQ](FAQ.md) | [Showcase](Showcase.md) | [Event descriptions](Event-descriptions.md) | [Configuration information](Configuration-information.md) | [Known Issues](Known-Issues.md) | [Possible features](Possible-features.md) | [Deprecations](Deprecations.md) | [Release notes](Release-notes.md) | [Helpful scripts](Helpful-scripts.md)
