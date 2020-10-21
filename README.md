# ngx-async-decorator

Decorator convert static input value to observable object

```
property<T> -> property<Observable<T>>
```

Use like

```
@Async() @Input('id') public readonly id$: Observable<string>|null = null;

or

@Async() @Input() public readonly id: Observable<string>|null = null;

```

Generate code:

```
  private destroyed$ = new Subject();
  public id$: Subject<string> = new Subject();
  @Input() id set(value) {
    this.id$.next(value);
  }
  public idStream$ = this.id$.pipe(
      takeUntil(this.destroyed$),
      publishReplay(1),
      refCount()
  )
```  
