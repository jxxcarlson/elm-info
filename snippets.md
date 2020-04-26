Joel Quenneville: did something like this when I had a search sent to a server that was triggered on input:

```
GotSearchInput str ->
 ( { model | currentSearch = str}
 , delaySearch str
 )
DelayComplete str ->
 if str == model.currentSearch then
   -- do expensive search
 else
   -- str is out of date, ignore
:100:
3
```

joelq  16 hours ago

```elm
delayInput : String -> Cmd Msg
delayInput str =
 Process.sleep 200
   |> Task.perform (\_ -> DelayComplete str)
```
