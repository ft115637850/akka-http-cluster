## An Example For Akka Cluster Working With Akka-http

Open three terminal windows.

In the first terminal window, start the first seed node with the following command:

    sbt "runMain cep.cluster.poc.Main 2551"

2551 corresponds to the port of the first seed-nodes element in the configuration. In the log output you see that the cluster node has been started and changed status to 'Up'.

In the second terminal window, start the second seed node with the following command:

    sbt "runMain cep.cluster.poc.Main 2552"

2552 corresponds to the port of the second seed-nodes element in the configuration. In the log output you see that the cluster node has been started and joins the other seed node and becomes a member of the cluster. Its status changed to 'Up'.

Switch over to the first terminal window and see in the log output that the member joined.

Start another node in the third terminal window with the following command:

    sbt "runMain cep.cluster.poc.Main 2553"

Start even more nodes in the same way, if you like.

Shut down one of the nodes by pressing 'ctrl-c' in one of the terminal windows. The other nodes will detect the failure after a while, which you can see in the log output in the other terminals.

Open a Rest Client to send GET request to the cluster with the following URL:

    http://localhost:2562/send

This will generate 10 job requests on the cluster. Send mutiple times, the job requests will be distributed according to nodes' workload.

Send another GET request to the cluster with the following URL:

    http://localhost:2562/query/ab9d8c18-5203-4919-a615-33c9de567e82
    
This will get the work status of the work request, the work ID of which, is ab9d8c18-5203-4919-a615-33c9de567e82. The work ID is returned by previous send request.
