# `reduxios`- Reduce your redux boilerplate by 80%

**This library providees utility functions specifically for handling reducers and actions related to data fetching which helps to decrease redux data fetching code by about 80%**

## Installation
```
npm i reduxios
# or
yarn add reduxios
```

## Example Usage in 4 simple steps

- **Generate the helper with the basename for action types**

```ts
import { reduxios } from "reduxios";

export const booksStoreFetcher = reduxios<Book[]>("FETCH_BOOKS");
```

-  **Create the Reducer, which will handle various Fetch states.
    It takes the initial data as an argument**

```ts
export const booksReducer = booksStoreFetcher.createReducer([]);
```

-  **Makes the action hook for Fetching your data or calling the API.**

```ts
import axios from "axios";

export const useFetchBooks = () => {
  return booksStoreFetcher.useResource({
    axiosInstance: axios, // This can also be an axios instance created
    method: "get",
    url: "/books"
  });
};
```

- **Use the action hook and state in your component. No need to dispatch the action.**

```tsx
const BooksList: FC = () => {
  const fetchBooks = useFetchBooks();
  const { data, fetchState, axiosErrorResponse } = useSelector(
    (state: RootState) => state.books
  );

  useEffect(() => {
    fetchBooks();
  }, []);

  return (
    <div>
      <h1>My Book List</h1>
      <ul>
        {data.map(book => (
          <Book key={book.id} book={book} />
        ))}
      </ul>
    </div>
  );
};
```

**That's it! No need to manually write out action creators, type declarations, reducers and data fetching attempt/success/failure/reset handling. You get everything out of the box!**

## Want More Detailed Explanation?

[Check the Github Repository here](https://github.com/Oyelowo/lib-steroids/tree/master/packages/reduxios-only)



