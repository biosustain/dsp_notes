# JavaDocs and Code Documentation

For users working with Nextflow, the **Nextflow extension for Visual
Studio Code** provides the best support for documentation and code
hints. Developers can include docstrings in their scripts, which will
enable hover-based code suggestions within the editor. Below is an
example of how to format a simple process using a docstring.

```java

\*
A simple process that outputs a "Hello, world!" message.
*/

process SAY_HELLO {

    tag "Saying hello"

    output:

        path "hello.txt", emit: hello_file

        path "versions.yml", emit: versions

    script:

    """

    echo \'Hello, world!\' \> hello.txt

    cat \<\<-END_VERSIONS \> versions.yml

    "say_hello": 1.0

    END_VERSIONS

    """

}

workflow {

    SAY_HELLO()

}
```

This approach helps ensure that developers can quickly reference process
definitions and outputs while working within Nextflow.

> Make sure you have Java 17 or above installed to make the VSCode extension work:
> [link](https://www.oracle.com/java/technologies/downloads)
