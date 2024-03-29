==================
 kubernetes notes
==================

Some notes taken while taking an edX course
`LinuxFoundationX LFS158x <https://learning.edx.org/course/course-v1:LinuxFoundationX+LFS158x+1T2022/home>`_ (Aug 2022).

The access token method described in the course does not work!

The problem seems to be that the `get secrets` command returns blank.
The method at the bottom works though, using the client certificate,
client key, and certificate authority as shown in the .kube/config file

Method that fails
-----------------

Command to obtain a token to authenticate to an api server::

  $ TOKEN=$(kubectl describe secret -n kube-system
           $(kubectl get secrets -n kube-system |
             grep default | cut -f1 -d ' ') |
             grep -E '^token' |
             cut -f2 -d':' |
             tr -d '\t' | tr -d " ")

The command to retrieve the api server endpoint::

  $ APISERVER=$(kubectl config view |
             grep https |
             cut -f 2- -d ":" |
             tr -d " ")

And to access the api server using 'curl', the command is::

  $ curl $APISERVER --header "Authorization: Bearer $TOKEN" --insecure

Method that works
-----------------
Instead of the access token, we can extract the client certificate,
client key, and certificate authority data from the .kube/config
file. Once extracted, they can be encoded and then passed with a curl
command for authentication. The new curl command would look similar to
the example below. Keep in mind, however, that the below example
command would only work with the encoded client certificate, key and
certificate authority data.::

  $ curl $APISERVER --cert encoded-cert \
          --key encoded-key --cacert encoded-ca

  
Storing urls about minikube
---------------------------

I still haven't managed to run a container generated by myself in a local minikube.
I want to do it eventually.
A search a week ago revealed something that seems relevant and I want to record:

* `How to use local docker images with Minikube? <https://stackoverflow.com/questions/42564058/how-to-use-local-docker-images-with-minikube>`_

I think the `search <https://duckduckgo.com/?t=ffab&q=minikube+docker+Dockerfile&ia=web>`_ 'minikube docker Dockerfile' was a good search.


