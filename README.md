<!--
    HTML generated from this Markdown file tested with:
        $ pandoc -f markdown_github -t html README.md > foo.html && c foo.html
-->        


# jar-zipgroupfileset-problem-SSCCE
[SSCCE][sscce] that demonstrates a problem with the `zipgroupfileset` Ant task that likely
tricks/confuses the [jar][jar] task into rebuilding its target.

## Description of the problem
(tested with Ant 1.9.9)

Using the `jar1` target as in: `ant jar1` causes the output artifact (`out.jar`)
to be built only once. Subsequent Ant runs (with the same `jar1` target) do not cause
a rebuild (unless the test jar files in the `some-jars` directory have in the meantime
been updated). This is as it should be.

However, when using the `jar2` target as in `ant jar2`, then the output artifact (`out.jar`)
is rebuilt **every time** Ant is run. The only difference between targets `jar1` and `jar2`
is that target `jar2` includes one additional jar file (`c.jar`) in its `zipgroupfileset`.


## original names of the test jar files used
For the record, these are the original names and provenance of the test jar
files that are used in the `some-jars` directory:
* `a.jar` is a rename of `commons-codec-1.9.jar`
* `b.jar` is a rename of `commons-io-2.5.jar`
* `c.jar` is a rename of `commons-logging-1.2.jar`

[sscce]: http://sscce.org/
[jar]: https://ant.apache.org/manual/Tasks/jar.html