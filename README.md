# python-pusher-client  
### pusher的Python客户端
Autobahn backed python pusher client

官方并没有提供Python的客户端，找了个实现了的。

项目fork自[ysobolev/python-pusher-client](https://github.com/ysobolev/python-pusher-client)  
修改有websocket的地址，改为wss协议，主机名有变化;send方法中对string编码.

其他的一些资料  
[ekulyk/PythonPusherClient](https://github.com/ekulyk/PythonPusherClient) issues中还有一些问题，没敢用  
[pusher websocket client，基于golang](https://blog.csdn.net/jeffrey11223/article/details/78698995) go版本

## Usage:
    import sys
    from twisted.internet import reactor
    from twisted.python import log

    from pusher_client import PusherClient
    bitstamp = PusherClient("de504dc5763aeef9ff52")
    
    def run(event, data):
        def on_data(channel, event, data):
            print(data)

        channel = bitstamp.subscribe("order_book")
        channel.bind("data", on_data)

    bitstamp.on("pusher:connection_established", run)

    log.startLogging(sys.stdout)
    reactor.run()

