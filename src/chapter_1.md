# About qml

QMl is a dsl for qt, it is like javascript, but a little noot like.

I wanner use qml to make a application like clash for windows.

What I need to learn is how to draw the view and animation.

## Attributes 

You can view the intruction from qt with this url 

[Attributes](https://doc.qt.io/qt-6/qtqml-syntax-objectattributes.html)

There are such keywords: required, properity and signals.

### properity and required

properity and required defined the properity when realized at first

```qmljs
// MyItem.qml
import QtQuick 2.0

Rectangle {
    // declaration without initialization
    property list<Rectangle> siblingRects

    // declaration with initialization
    property list<Rectangle> childRects: [
        Rectangle { color: "red" },
        Rectangle { color: "blue"}
    ]
}
```

```qmljs 
Application {
	Rectangle {
		siblingRects : []
	}
}
```

If used required, such properity is must be defined.

### signals and slots

Signals in qml is the same as the same things in cpp. Just use the example on qt 

```qmljs 
// SquareButton.qml
Rectangle {
    id: root

    signal activated(xPosition: real, yPosition: real)
    signal deactivated

    property int side: 100
    width: side; height: side

    MouseArea {
        anchors.fill: parent
        onReleased: root.deactivated()
        onPressed: (mouse)=> root.activated(mouse.x, mouse.y)
    }
}
```

```qmljs 
// myapplication.qml
SquareButton {
    onDeactivated: console.log("Deactivated!")
    onActivated: (xPosition, yPosition)=> console.log("Activated at " + xPosition + "," + yPosition)
}
```
