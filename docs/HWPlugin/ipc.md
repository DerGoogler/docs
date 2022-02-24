# IPC (Beta)

## On

```js
ipc.on("myEvent", (data) =>
    console.log(data.message);
);
```

## Send

```js
ipc.send("myEvent", { message: "Pong" });
```

## Destroy

```js
ipc.destroy("myEvent");
```