Authentication顾名思义是验证 “谁是用户，用户是谁”的一套逻辑。返回的也自然是:

- 如果不是用户或用户不是被授权的，那则是identity not confirmed，也就是401 unauthorized
- 如果通过了，则可以继续请求
  所以其基本逻辑是

1. 通过不同的[Authentication Method](Authentication%20Method.md)，进行验证拿到凭证
2. 使用获得的凭证进行[Authentication Session Management](Authentication%20Session%20Management.md)
