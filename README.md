# wenexus-module-guide
Contains wenexus module guide.

<br>

### Use Better Fetcher
* `useBetterFetcher` is a layer of remix's `useFetcher`.
* It has `useFetcher`'s functionality but designed to solve something more.
* It has `shopify-loading` feature and has good error handling. What if there is any error, this `betterFetcher` lets user know something went wrong.
* You can use `betterFetcher` to submit a form.
```typescript jsx
import { useBetterFetcher } from '~/hooks/use-better-fetcher';
import { useCallback } from "react";

const Component = () => {
  const fetcher = useBetterFetcher();
  
  const formData = new FormData();
  formData.append("firstName","john");

  const clickHandler = useCallback(() => {
    fetcher.submit({
        loading: true, // should I show loading/progress bar at the top
        toast: true, // show toast if there is any error.
      },
      formData,
      {
        method: "POST", 
        action: "/api/test" // where do you want to send the submit request.
        // .. here you can add all the other option argument which `useFetcher` has.
      }
    ).then((res) => {
      console.log(res);
    }).catch(e => console.log(e));
  }, [])



  return(
    <>
      <button onClick={clickHandler}>
        Click me!
      </button>
    </>
  )
}
```

##### More usage 
* You can set payload to `null` if you don't want to send any data.
```typescript jsx
fetcher.submit({
    loading: true, // should I show loading/progress bar at the top
    toast: true, // show toast if there is any error.
  },
  null,
  {
    method: "POST", 
    action: "/api/test" // where do you want to send the submit request.
    // .. here you can add all the other option argument which `useFetcher` has.
  }
)
```
<br>

* You can use `useBetterFetcher` to do more operation like `load`, read `fetcher state` etc.
```typescript jsx
import { useBetterFetcher } from '~/hooks/use-better-fetcher';

const Component = () => {
  /**
   * you can either destruct properties or get as single object. 
   * You can follow one of these two.
   **/
  const {fetcher, submit} = useBetterFetcher();
  const fetcher_ = useBetterFetcher();
  
  useEffect(() => {
    // submit something
    // fetcher_.submit(....)
    // submit(...) --- similar to fetcher_.submit
  }, [])

  useEffect(() => {
    // load something
    // fetcher_.fetcher.load(....)
    // fetcher.load(...) --- similar to fetcher_.submit 
  }, [])
}
```

#### New Update
* You can show `toast message` after operation is successful.

