# Publish / Async-Response 

The publish/async responses interaction style is a higher-level style of interaction that’s
implemented by combining elements of publish/subscribe and request/response. A cli-
ent publishes a message that specifies a reply channel header to a publish-subscribe
channel. A consumer writes a reply message containing a correlation id to the reply
channel. The client gathers the responses by using the correlation id to match the reply
messages with the request.

![link](https://media-exp1.licdn.com/dms/image/C4E12AQEy1j6TUv884Q/article-inline_image-shrink_1500_2232/0/1583202180201?e=1647475200&v=beta&t=9QpcPoKE9N--agE6amMBcyiIQJhMyFSGy2ftjKpdJ-w);