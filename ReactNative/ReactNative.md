[react-native-clean-project](https://github.com/pmadruga/react-native-clean-project)

| State Type            | Command                         | In clean-project-auto? | Optional? | Default?                 | Option Flag                  |
| --------------------- | ------------------------------- | ---------------------- | --------- | ------------------------ | ---------------------------- |
| React-native cache    | rm -rf $TMPDIR/react-*          | Yes                    | No        | true                     |
| Metro bundler cache   | rm -rf $TMPDIR/metro-*          | Yes                    | No        | true                     |
| Watchman cache        | watchman watch-del-all          | Yes                    | No        | true                     |
| NPM modules           | rm -rf node_modules             | Yes                    | Yes       | true                     | --keep-node_modules          |
| Yarn cache            | yarn cache clean                | Yes                    | Yes       | true                     | --keep-node-modules          |
| Yarn packages         | yarn install                    | No                     | Yes       | true                     | --keep-node-modules          |
| NPM cache             | npm cache verify                | Yes                    | Yes       | true	--keep-node-modules |
| NPM Install           | npm ci                          | Yes                    | Yes       | true                     | --keep-node-modules          |
| iOS build folder      | rm -rf ios/build                | Yes                    | Yes       | false                    | --remove-iOS-build           |
| iOS pods folder       | rm -rf ios/Pods                 | Yes                    | Yes       | false                    | --remove-iOS-pods            |
| system iOS pods cache | pod cache clear --all           | Yes                    | Yes       | true                     | --keep-system-iOS-pods-cache |
| user iOS pods cache   | rm -rf ~/.cocoapods             | Yes                    | Yes       | true                     | --keep-user-iOS-pods-cache   |
| Android build folder  | rm -rf android/build            | Yes                    | Yes       | false                    | --remove-android-build       |
| Android clean project | (cd android && ./gradlew clean) | Yes                    | Yes       | false                    | --clean-android-project      |
| Brew package          | brew update && brew upgrade     | No                     | Yes       | true                     | --keep-brew                  |
| Pod packages          | pod update                      | No                     | Yes       | true                     | --keep-pods                  |



### Pure Component
Pure là nguyên thuỷ không thây đổi
React.Component có shouldComponentUpdate: default => true => Component luôn update
=> custom shouldComponentUpdate để tránh render không cần thiết
Ngoài ra, dùng Pure Component (có sẵn shouldComponentUpdate với shallowEqual)

```javascript
if (type.prototype && type.prototype.isPureReactComponent) {
  shouldUpdate = !shallowEqual(oldProps, props) || !shallowEqual(oldState, state);
}

function shallowEqual(objA: mixed, objB: mixed): boolean {
  if (is(objA, objB)) {
    return true;
  }

  if (typeof objA !== 'object' || objA === null ||
      typeof objB !== 'object' || objB === null) {
    return false;
  }

  const keysA = Object.keys(objA);
  const keysB = Object.keys(objB);

  if (keysA.length !== keysB.length) {
    return false;
  }

  // Test for A's keys different from B.
  for (let i = 0; i < keysA.length; i++) {
    if (
      !hasOwnProperty.call(objB, keysA[i]) ||
      !is(objA[keysA[i]], objB[keysA[i]])
    ) {
      return false;
    }
  }

  return true;
}
```

### Shallow equality
> Performs equality by iterating through keys on an object and returning false when any key has values which are not strictly equal between the arguments. Returns true when the values of all keys are strictly equal.
```
const value = 'cat';

const item1 = value;
const item2 = value;

console.log(item1 === item2); // true

const array1 = [value];
const array2 = [value];

console.log(array1 === array2); // false
```

### Deep(strictly) equality
``` 
const value = 'cat';

const array1 = [value];
const array2 = [value];

let equal = true;
array1.forEach((item, index) => {
    equal = equal && array1[index] === array2[index];
});

console.log(equal); // true
```

=> Shallow sẽ nhanh hơn, performance tốt hơn
=> Cần chú ý một số trường hợp sẽ không re-render như ý

### useMemo, useCallback

useMemo trả ra 1 memoized **value**
useCallback trả ra 1 memoized **function**  

```javascript
const returnedFunction = useCallback(fn, deps);
const returendValue = useMemo(fn, deps);

useCallback(fn, deps) === useMemo(() => fn, deps);
```

Functional Component không có life cycle như Class Component
mọi thứ bên trong Functional Component chính là body của hàm render
=> Functional Component re-render => các hàm và logic sẽ được tính toán lại
các hàm là object nên re-render sẽ tạo object mới => các component con có props là các hàm đó bị re-render theo, mặc cho các component con đó có áp dụng React.memo hay React.PureComponent

- Tính toán nặng
```javascript
const componentA = () => {
  const [count, setCount] = useState(0);

  const getArray = () => {
    // tưởng tượng một hàm phức tạp, filter,
    // sort một mảng 100 phần tử, tốn 2s để chạy
    const result = filterAndSortAndDoSomething(...);
    return result;
  }

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      <div>mảng phức tạp: {getArray()}</div>
    </div>
  )
}
```
click tăng count => re-render và getArray chạy lại => đợi 2s để có kết quả và render ra màn hình

```javascript
const componentA = () => {
  const [count, setCount] = useState(0);

  const getArray = useMemo(() => {
    // tưởng tượng một hàm phức tạp, filter,
    // sort một mảng 100 phần tử, tốn 2s để chạy
    const result = filterAndSortAndDoSomething(...);

    return result;
  }, []);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      <div>mảng phức tạp: {getArray}</div>
    </div>
  )
}
```
click tăng count => re-render và getArray trả về kết quả trước đó đã lưu => render ra màn hình ngay

- Tránh re-render
```javascript
const ComponentA = () => {
  const getStyle = () => {
    return {
      color: 'blue',
      background: 'gold',
    };
  };

  return (
    <div>
      CHA NÈ CON
      <ComponentB myStyle={getStyle()} />
    </div>
  );
};

const ComponentB = React.memo(props => {
  return <div style={props.myStyle}>CON NÈ CHA</div>;
});
```
ComponentA re-render => hàm getStyle sẽ tạo ra một object mới và pass xuống ComponentB => ComponentB bị re-render theo (mặc dù đã sử dụng React.memo)

```javascript
const ComponentA = () => {
  const getStyle = useMemo(() => {
    return {
      color: 'blue',
      background: 'gold',
    };
  }, []);

  return (
    <div>
      CHA NÈ CON
      <ComponentB myStyle={getStyle} />
    </div>
  );
};
****
const ComponentB = React.memo(props => {
  return <div style={props.myStyle}>CON NÈ CHA</div>;
});
```
ComponentA re-render => hàm getStyle trả ra object style cũ thay vì tạo mới => ComponentB không re-render, vì React.memo nhận thấy props không có sự thay đổi

- useCallback - Tránh re-render ở component con
```javascript
function Parent({ ... }) {
  const [a, setA] = useState(0);
  const onChangeHandler = () => {
    doSomething(a);
  };
  ...
  return (
    ...
    //Pure là component con có sử dụng React.memo
    <Pure onChange={onChangeHandler} />
  );
}
```
Component Parent re-render => callback onChangeHandler sẽ được tạo mới và pass xuống component con Pure => Pure bị re-rendered.

```javascript
function Parent({ ... }) {
  const [a, setA] = useState(0);
  const onChangeHandler = useCallback(() => {
    doSomething(a);
  }, [a]);
  ...
  return (
    ...
    //Pure là component con có sử dụng React.memo
    <Pure onChange={onChangeHandler} />
  );
}
```
Component Parent re-render => hàm onChangeHanlder sẽ không còn luôn luôn bị tạo mới nữa, mà sẽ chỉ được tạo mới khi depencency của nó là biến a thay đổi -> Function không bị tạo mới -> object không bị tạo mới -> Pure không bị re-render

https://reactnative.dev/docs/performance

https://stackoverflow.com/questions/46126521/android-navigation-bar-height-react-native
https://stackoverflow.com/questions/44978804/whats-the-difference-between-window-and-screen-in-the-dimensions-api


- redux, lifecycle của component: biết cách hoạt động và áp dụng, vẫn còn thiếu sót một số methods
- hook: dùng các hooks ở mức cơ bản, có một số hook cơ bản chưa xài tới, 
- custom hook chưa nhiều nên vẫn chưa áp dụng được với các side effect, 3 party, firebase...
- optimize performance: biết cách dùng một số kỹ thuật nhưng chưa áp dụng nhiều
- library: kinh nghiệm với 3 party lib, upgrade lib, xử lý issue cho ở mức cơ bản
- deployment: ok, CI/CD chưa làm
- native module: chưa làm nhiều
- others: chưa làm việc nhiều với những component phức tạp, cách implemment 1 component mới vẫn chưa được thấu đáo (UI/UX, flow data, override style)
Overall: level ở mức standard+ 

- redux, component lifecycle: know how to work and apply, still missing some methods
- hooks: can use basic hooks fairly
- Not much experience on Custom hook, thus he's not able to handle side effects, 3 parties, firebase...
- optimize performance: know how to use some techniques with liminted experience
- library: familiar with 3 party libs, libs upgradng, handle issues on basic level
- deployment: decent skill, unfamiliar with CI/CD
- native module: little experience
- others: haven't worked much with complex components, not fully understood the way to implement a new component (UI/UX, data flow, override style)
Overall: his level is at standard+