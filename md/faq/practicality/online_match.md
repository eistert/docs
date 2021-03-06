# 在线交友
现在是快餐时代，交友也是一样，像过去那样交笔友来往一次需要2周时间的日子已经一去不复返了。在线交友就是双方实时在线，3秒钟匹配成功，如果要是超过几分钟，可能就有人等得不耐烦了。这对技术提了很高的要求。

## 使用IM在线状态的问题
提供匹配的成功率的关键在于准确的知道用户是否在线，自然而然的想到如果使用IM的在线状态不就能达到目标了吗？但其实IM在线状态并不适合，原因有如下几点：

1. IM在线状态有时并不准确。IM客户端与IM服务器是通过长连接保持联系，在某些特殊的情况下，服务器并不知道客户端已经断开，只有通过心跳超时才能知道已经不在线。心跳超时的时间大概在5分钟左右，可能用户在3分钟之前已经离开，但再也不会回来了。

2. IM在线状态不能表明程序打开状态。android的环境非常复杂，我们的应用在有些手机的后台能存活非常长的时间，而在有些手机上则会很快被杀掉。即使在线，应用也可能是在后台的状态，客户已经不太关注了。

3. IM在线状态不能附带用户交友意愿。可能应用中会有各种状态，比如我像“立即开始聊天”和”我先瞎逛逛“之类的状态，这就不能完全依赖IM的在线状态。还是需要把这些信息同步到服务器。

4. IM在线状态不能附带用户的地理位置信息。可能应用中还要根据用户的IP或者地理位置来匹配。以此类推，可能还有性别，爱好，星座等。还是需要同步到应用服务器的。

## 我们推荐的做法：
在应用服务器上做，在适当的界面和时机（比如前台，状态为立即交友）以每分钟一次的频率提交交友请求（可以付费客户和免费客户不同的频率）。在服务器端收到交友请求，从redis里获取最新随机的状态，更新匹配结果，返回结果（之后的处理方式可能是请求方发送一条自定义消息给对方，对方收到消息弹出界面，是否开始交友。。。）。如果找不到匹配对象，更新请求到redis里去，等待别人匹配成功。在离开的界面发送取消交友请求，清除掉服务器的交友请求。为了防止状态不正确，可以使用redis的过期机制，交友信息一分钟过期，这样就能保证准确性。
