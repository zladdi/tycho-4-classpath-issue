# tycho-4-classpath-issue
Repository to demonstrate a specific classpath issue at build time with Tycho 4

## System requirements
* JDK 17 (e.g. AdoptOpenJDK 17)
* Maven 3.9.9 (a higher version might work, but has not been tested)

## Building the project to reproduce the error

`mvn -B clean verify -DskipTests -Dtycho.localArtifacts=ignore`

The expected error one gets is:

```
[ERROR] Failed to execute goal org.eclipse.tycho:tycho-compiler-plugin:4.0.10:compile (default-compile) on project dependent: Compilation failure: Compilation failure:
[ERROR] <parent-of-repo>/tycho-4-classpath-issue/dependent/src/DependentExample.java:[1]
[ERROR]         import org.apache.commons.lang3.StringUtils;
[ERROR]                ^^^^^^^^^^
[ERROR] The import org.apache cannot be resolved
[ERROR] <parent-of-repo>/tycho-4-classpath-issue/dependent/src/DependentExample.java:[9]
[ERROR]         boolean sIsBlank = StringUtils.isBlank(s);
[ERROR]                            ^^^^^^^^^^^
[ERROR] StringUtils cannot be resolved
[ERROR] <parent-of-repo>/tycho-4-classpath-issue/dependent/src/DependentExample.java:[12]
[ERROR]         System.out.println("bitfield is: " + dependeeEx.getBitField());
[ERROR]                                              ^^^^^^^^^^^^^^^^^^^^^^^^
[ERROR] The type org.apache.commons.lang3.BitField cannot be resolved. It is indirectly referenced from required type dependee.DependeeExample
[ERROR] <parent-of-repo>/tycho-4-classpath-issue/dependent/src/DependentExample.java:[12]
[ERROR]         System.out.println("bitfield is: " + dependeeEx.getBitField());
[ERROR]                                                         ^^^^^^^^^^^
[ERROR] The method getBitField() from the type DependeeExample refers to the missing type BitField
[ERROR] 4 problems (4 errors)
[ERROR] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoFailureException
[ERROR]
[ERROR] After correcting the problems, you can resume the build with the command
[ERROR]   mvn <args> -rf :dependent
```
