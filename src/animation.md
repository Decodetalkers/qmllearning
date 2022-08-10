# Animation

Qt 的动画这里我将qml和qtwidget的动画方式进行介绍，同时会介绍statemachine的状态管理机器。

在介绍这些事情之前，需要介绍qt的属性porperty,在cpp中以类似放好似呈现

```cpp
Q_PROPERTY(qreal positiony WRITE setPositionY READ positiony NOTIFY updatepositon)
```

这行定义了传入的类型，写的函数，读的函数，以及内容更新后的signal。如果是cpp到qml,qml需要知道你消息更新了然后更新qml中数据，所以当需要数据更新时候，emitChanged是不可少的,这个会将消息更新，然后在ui上更新

qt这个设计让cpp的object更加类似json,或者说qt 梦想的cpp就是javascript的样子。这时候使用setProxy 就可以设置object的属性了。

## State 

状态机。qt中使用状态机保存和管理控件状态。statemechine可以用来实现复杂的动画和状态变化。其中有两个重要的参数

```cpp
QSignaltransition *transition;
QPropertyAnimation *transition;
```

QSignaltransition 是连接两个target的变化。其中有两个重要函数

```cpp 
transition->setTargetState(m_target_state); // target state 
m_start_transition->addTransition(transition); // transition 
```

上述代码描述了从m\_target\_state 到m\_target\_state的变化。定义了出发的signal。

```cpp ,editable
animation = new QPropertyAnimation(m_mime, "positionx", this);
animation->setDuration(420);
animation->setEasingCurve(QEasingCurve::OutCurve);
transition->addTransition(animation);
```

上述代码定义了变化的动画，定义了变化的属性，时长，变化方式，最后将动画加到transition中。

使用Statechine时候需要先定义初始状态，然后start，就可以管理状态了，详情可以看qt的state 例子

## qml 

qml 中同样有state等行为
