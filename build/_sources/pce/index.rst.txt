Path Computation Engine (PCE)
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

Introduction
@@@@@@@@@@@@

Most of the logic for path computation resides in the services/src/pce project.

The initial implementation of the path algorithm relies on the mechanisms native to Neo4J - i.e. we have an abstraction for a path computer, and the initial / default implementation is Neo4J. The Neo4J driver is just a thin facade.

Testing
@@@@@@@

Acceptance Tests
################

There are a couple of Acceptance Tests that exercise this code base:

FlowPathTest.java

PathComputationTest.java

These are in the atdd project in

``services/src/atdd .. src/test``

Unit Tests
##########

The PCE project has multiple unit tests that excercise most / all of the core logic.

Development
###########

Here are the basic steps to getting up and running:

1. Ensure you can run this maven project, run the tests, and they all should pass.
2. Ensure you can run the acceptance tests:

   ``make atdd tags="@PCE,@FPATH"``

Notes
@@@@@

In addition to this sparse guide, there are more notes in PathComputationTests.java regarding how the acceptance is executed. That should give you a good guide to how the code comes together.

SimpletGetShortestPath Algorithm
Source: ``open-kilda/services/src/pce/src/main/java/org/openkilda/pce/algo``

This algorithm is optimized for finding a bidirectional path between the start and end nodes.

  * It uses elements of depth first, breadth first, and shortest path (weight) algorithms.

For neighboring switches, it assumes there is only one link between them. The network that is

  * passed in should reflect the links that should be traversed.

Algorithm Notes
###############

::

   1. forward = get path (src, dst)
   2. reverse = get path (dst, src, hint=forward)
   3. get path:
   
        0. allowedDepth = 35
        √ . go breadth first (majority of switches probably have 5 hops or less)
        √ . add cost
        . compare against bestCost (if greater, then return)
        . have we visited this node before?
            - if so, was it cheaper? Yes? return.
            - No, remove the prior put. We
          and any downstream cost (BUT .. maybe we stopped somewhere and need to continue?
          Probably could just replace the old one with the current one and add the children as unvisited?
          Oooh .. this could cause a loop.. if there are negative costs
            - So, should probably track path to this point...
        . if node = target, update bestCost, return
        . add each neighbor to the investigation list, where neighbor.outbound.dst != current node.

SimpleISL

Call this method to find a path from start to end (srcDpid to dstDpid), particularly if you

have no idea if the path exists or what the best path is.
An ordered list that represents the path from start to end, or an empty list will be returned

::

   */

   / Determine if this node is the destination node.   We found the destination    We found a best path. If we don't get here, then the entire graph will be
                   searched until we run out of nodes or the depth is reached.

 We found dest, no need to keep processing

 Otherwise, if we've been here before, see if this path is better    We've already visited this one .. keep going only if this is cheaper

 Either this is the first time, or this is cheaper .. either way, this node should
             be the one in the visited list

 Stop processing entirely if we've gone too far, or over bestCost

 At this stage .. haven't found END, haven't gone too deep, and we are not over cost.
             So, add the outbound isls.

This is generally called after getPath() to find the path back.  The path back could be
asymmetric, but this will increase the odds that we return the symmetric path if it exists.
The hint will be used to determine if it exists.  If it does, then use it as the start
bestCost and bestPath.  That should help speed things along.
Whereas it's possible that could build up the SearchNodes for this path (if found) and put

them into the visited bucket, we'll start without that optimization and decide later whether
adding it provides any efficiencies
