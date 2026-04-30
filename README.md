# How to run

```
npm i
npm run dev
```

# What happens

R3F leaks the last root's state via module-level variables in the render loop.

After all Canvas components unmount and _roots is empty, the module-scoped `state`, `subscribers`, and `subscription` variables in the loop/update functions still reference the last rendered root's store state — preventing GC of the entire fiber tree and any bridged context values.

Repro: click the button, wait for all 16 cycles, observe last value stays "alive".
