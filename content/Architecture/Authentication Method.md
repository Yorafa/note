最基础的的auth method有:

1. Basic: 在每次request时附上自己的credentials，一般来说时经过[base64](/Algorithm%20&%20Data%20Structure/Base64)加密。也因此不再被经常使用了
2. Digest: 与Basic类似，不过经过MD5 hash，但也一样不再被经常使用了
3. Api Keys: client生成unique的api key，然后接下来的每次请求都会使用这个api key
