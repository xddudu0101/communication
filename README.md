# communication
同一个页面之间的2个组件使用signals实现通信

我们会发现，signals应用很简单，步骤为：

      1：先创建一个signals.Signal的实例对象。
        var myObject = {
                          started : new signals.Signal()
                        };
        function onStarted(param1, param2){
                            alert(param1 + param2);
                          }

      2：该对象通过dispatch()方法发布数据。
        myObject.started.dispatch('foo', 'bar');

      3：该实例对象提供add(function(data){})方法监听到数据,data默认为发布的数据。
        myObject.started.add(onStarted); //add listener

      4：如果需要，可以通过remove()关闭连接。
        myObject.started.remove(onStarted); //remove a single listener
        

        
