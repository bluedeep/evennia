# 门户与服务器

```
Internet│  ┌──────────┐ ┌─┐           ┌─┐ ┌─────────┐
        │  │Portal    │ │S│   ┌───┐   │S│ │Server   │
    P   │  │          │ │e│   │AMP│   │e│ │         │
    l ──┼──┤ Telnet   ├─┤s├───┤   ├───┤s├─┤         │
    a   │  │ Webclient│ │s│   │   │   │s│ │ Game    │
    y ──┼──┤ SSH      ├─┤i├───┤   ├───┤i├─┤ Database│
    e   │  │ ...      │ │o│   │   │   │o│ │         │
    r ──┼──┤          ├─┤n├───┤   ├───┤n├─┤         │
    s   │  │          │ │s│   └───┘   │s│ │         │
        │  └──────────┘ └─┘           └─┘ └─────────┘
        │Evennia
```

_Evennia_ 的两个主要部分由 _Portal_ 和 _Server_ 组成。

这两个是独立的 `twistd` 进程，可以从游戏内部或命令行控制，具体描述请参见 [Running-Evennia 文档](../Setup/Running-Evennia.md)。

- 门户（Portal）了解所有关于互联网协议（如 telnet、websockets 等）的知识，但对游戏知之甚少。
- 服务器（Server）了解关于游戏的一切。它知道玩家已连接，但不知道他们是 _如何_ 连接的。

这样做的效果是，你可以完全 `reload` 服务器，而玩家仍然保持连接。当服务器重新启动时，它会重新连接到门户并重新同步所有玩家，就像什么都没发生过一样。

门户和服务器旨在始终在同一台机器上运行。它们通过 AMP（异步消息协议）连接粘合在一起。这使得两个程序可以无缝通信。
