# Assignment: Zookeeper Tester System How-to

This document provides instructions on how to use the "Tester System". Similar test cases will be used to grade student submissions. For assignment submission, please follow the original instructions.

## Running the Tester

1. Extract the contents of "zookeeper_student.tar.gz"

2. Package your solution by running "package.sh" in your starter code directory

3. Rename your packaged tar.gz file to `group_YOURGROUPNUMBER.tar.gz`

4. Copy the tar.gz file to `subs/` directory in the testing directory (zookeeper_student/)

5. Modify `zookeeper.config`. Change 10378 and 10379 to different numbers within 10000 - 11000 ranges to avoid port collision from other students

6. Run the "test_your_solution.sh" script. It may take a few minutes

7. Example terminal output:

    ```
    --- Creating ZooKeeper node
    --- Cleaning
    --- Compiling Thrift IDL
    Thrift version 0.13.0
    --- Compiling Java
    javac 11.0.23
    Note: lib/zookeeper-3.4.13.jar(/org/apache/zookeeper/server/quorum/QuorumPeer.java) uses or overrides a deprecated API.
    Note: Recompile with -Xlint:deprecation for details.
    [main] INFO org.apache.curator.utils.Compatibility - Running in ZooKeeper 3.4.x compatibility mode
    [main] INFO org.apache.curator.utils.Compatibility - Using emulated InjectSessionExpiration
    [main] INFO org.apache.curator.framework.imps.CuratorFrameworkImpl - Starting
    [main] DEBUG org.apache.curator.CuratorZooKeeperClient - Starting
    [main] DEBUG org.apache.curator.ConnectionState - Starting
    [main] DEBUG org.apache.curator.ConnectionState - reset
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:zookeeper.version=3.4.13-5build1--1, built on Tue, 18 Feb 2020 10:26:56 +0100
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:host.name=ecetesla2.uwaterloo.ca
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:java.version=11.0.23
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:java.vendor=Ubuntu
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:java.home=/usr/lib/jvm/java-11-openjdk-amd64
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:java.class.path=.:lib/curator-framework-4.3.0.jar:lib/slf4j-api-1.7.25.jar:lib/curator-recipes-4.3.0.jar:lib/curator-client-4.3.0.jar:lib/guava-jar-lib/guava-27.0-jre.jar:lib/jsr305-3.0.2.jar:lib/error_prone_annotations-2.1.3.jar:lib/commons-logging-1.2.jar
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:java.library.path=/usr/java/packages/lib:/usr/lib/x86_64-linux-gnu/jni:/lib/x86_64-linux-gnu:/usr/lib/x86_64-linux-gnu:/usr/lib/jni:/lib:/usr/lib
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:java.io.tmpdir=/tmp
    [main] INFO org.apache.zookeeper.ZooKeeper - Client environment:java.compiler=<NA>
    ```

8. The tester will also produce log files (.log) and result summaries (.txt) in the result directory

### Tips for Troubleshooting

If you encounter permission errors while executing shell scripts, update permissions by running `chmod +x <script_name>.sh`.

## Test Cases

### Overview

The tester system tests various scenarios by periodically terminating the primary and backup processes. Ideally, your solution should have 0 linearizability violations across all tests and achieve good throughput.

### Case 1: Small Key space, Terminating Primary

**Inputs:**

-   numThreads = 4
-   keyspaceSize = 100
-   Terminating Interval = 5s

**Passing Criteria:** The backup process should correctly step up as the new primary process, the primary process should replicate its data to the backup process.

### Case 2: Small Key space, Terminating Secondary

**Inputs:**

-   numThreads = 4
-   keyspaceSize = 100
-   Terminating Interval = 5s

**Passing Criteria:** You solution should not experience any linearizability violation.

### Case 3: Medium Key space, Terminating Primary

**Inputs:**

-   numThreads = 4
-   keyspaceSize = 1,000
-   Terminating Interval = 4s

**Passing Criteria:** Larger keyspace, shorter time to back up everything.

### Case 4: Larger Key space, Terminating Primary

**Inputs:**

-   numThreads = 4
-   keyspaceSize = 10,000
-   Terminating Interval = 4s

### Case 5: Even Larger Key space, Terminating Primary

**Inputs:**

-   numThreads = 4
-   keyspaceSize = 100,000
-   Terminating Interval = 4s
