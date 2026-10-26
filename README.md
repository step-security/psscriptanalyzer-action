[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# PSScriptAnalyzer Action
Github action for running PSScriptAnalyzer and use ConvertToSARIF to generate a SARIF file.

# Getting Started
To run this action add the step below in your GitHub Action:
```yaml
 - name: Run PSScriptAnalyzer
   uses: step-security/psscriptanalyzer-action@v1
   with:
    path: .\
    recurse: true 
    output: results.sarif
```
The above yaml code scans all the code in your repository and outputs the results to `result.sarif` at the CWD.

# YAML
See the [input section](#Inputs) for more info about the inputs.
```yaml
 - name: Run PSScriptAnalyzer
   uses: step-security/psscriptanalyzer-action@v1
   with:
    path:
    customRulePath: 
    recurseCustomRulePath: 
    excludeRule: 
    includeDefaultRules:
    includeRule:
    severity:
    recurse:
    suppressedOnly:
    fix:
    enableExit:
    settings:
    output:
    ignorePattern:
```

# Inputs
The inputs for the action. The inputs `output` and `ignorePattern` are action specific. The rest are mapped to the parameters of PSScriptAnalyzer.
Every input is of type string. 

To provide an array follow the format `'"value.fake", "value1.fake", ....'`
## path
Specifies the path to the scripts or module to be analyzed. Wildcard characters are supported. Default value is: `.\`. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-path).
```yaml
with:
  path: .\
```
```yaml
with:
  path: .\src
```
## customRulePath
Specifies the path to the scripts or module to be analyzed. Wildcard characters are supported. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-customrulepath).
```yaml
with:
  customRulePath: '".\customRule.ps1"'
```
```yaml
with:
  customRulePath: '".\customRule.ps1", "customRule2.ps1"'
```

## recurseCustomRulePath
Uses only the custom rules defined in the specified paths to the analysis. To still use the built-in rules, add the -IncludeDefaultRules switch. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-recursecustomrulepath).
```yaml
with:
  recurseCustomRulePath: true
```
```yaml
with:
  recurseCustomRulePath: false
```

## excludeRule
Omits the specified rules from the Script Analyzer test. Wildcard characters are supported. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-excluderule).
```yaml
with:
  # exclude one rule 
  excludeRule: '"PSAvoidLongLines"'
```
```yaml
with:
  # exclude multiple rules
  excludeRule: '"PSAvoidLongLines", "PSAlignAssignmentStatement"'
```

## includeDefaultRules
Uses only the custom rules defined in the specified paths to the analysis. To still use the built-in rules, add the -IncludeDefaultRules switch. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-includedefaultrules).
```yaml
with:
  includeDefaultRules: true 
```
```yaml
with:
  includeDefaultRules: false
```

## includeRule
Runs only the specified rules in the Script Analyzer test. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-includerule).
```yaml
with:
  # Include one rule
  includeRule: '"PSAvoidUsingInvokeExpression"'
```
```yaml
with:
  # Include multiple rules
  includeRule: '"PSAvoidUsingInvokeExpression", "PSAvoidUsingConvertToSecureStringWithPlainText"' 
```

## severity
After running Script Analyzer with all rules, this parameter selects rule violations with the specified severity. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-severity).
```yaml
with:
  # Report only rule violations with error severity
  severity: '"Error"'
```
```yaml
with:
  # Report only rule violations with error and warning severity
  severity: '"Error", "Warning"'
```
## recurse
Script Analyzer on the files in the Path directory and all subdirectories recursively. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-recurse).
```yaml
with:
  recurse: true
```
```yaml
with:
  recurse: false
```

## suppressedOnly
Returns rules that are suppressed, instead of analyzing the files in the path. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-suppressedonly).
```yaml
with:
  suppressedOnly: true
```
```yaml
with:
  suppressedOnly: false
```

## fix
Fixes certain warnings which contain a fix in their DiagnosticRecord. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-fix).
```yaml
with:
  fix: true
```
```yaml
with:
  fix: false
```

## enableExit
Exits PowerShell and returns an exit code equal to the number of error records. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-enableexit).
```yaml
with:
  enableExit: true
```

```yaml
with:
  enableExit: false
```

## settings
File path that contains user profile or hash table for ScriptAnalyzer. Does not support passing a hashtable as an argument. More info [here](https://github.com/PowerShell/PSScriptAnalyzer/blob/master/docs/Cmdlets/Invoke-ScriptAnalyzer.md#-settings).
```yaml
with:
  settings: .\settings.psd1
```

## output
File path that defines where the SARIF output will be stored.
```yaml
with:
  output: results.sarif
```

## ignorePattern
Exclude specific files from the SARIF results. Uses regex pattern.
```yaml
with:
  # Any file or folder that have the name test will not be present in the SARIF file.
  ignorePattern: 'tests'
```
