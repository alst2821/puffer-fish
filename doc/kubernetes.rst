==================
 kubernetes notes
==================

Some notes taken while taking an edX course
`LinuxFoundationX LFS158x <https://learning.edx.org/course/course-v1:LinuxFoundationX+LFS158x+1T2022/home>`_ (Aug 2022).

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

Instead of the access token, we can extract the client certificate, client key, and certificate authority data from the .kube/config file. Once extracted, they can be encoded and then passed with a curl command for authentication. The new curl command would look similar to the example below. Keep in mind, however, that the below example command would only work with the encoded client certificate, key and certificate authority data.::

  $ curl $APISERVER --cert encoded-cert \
          --key encoded-key --cacert encoded-ca

  
