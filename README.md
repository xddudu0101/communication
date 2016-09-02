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
        

 html页面中的关键代码为：
      1.全局创建sianal对象
         //设置数据广播
         var broadData=new signals.Signal(); //全局数据广播对象
         var datas={};  //总数据对象 
         
      2.进度条组件：加入监听函数从setState中获取数据
         broadData.add(function(data){ //收听到数据
                   that.setState({
                      endValue:data.curValue,
                   });
                });
      3.输入框组件：将数据放入broadData中    
            getEndValue:function(){
                          var curValue=this.refs.endValue.value;
                          if(curValue <= 0) curValue=0;
                          if(curValue >=100) curValue=100;
                          datas.curValue=curValue; //将curValue放入总数居对象
                          broadData.dispatch(datas); //发布数据
                         
            },
      
