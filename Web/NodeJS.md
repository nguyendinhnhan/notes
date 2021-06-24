* install MongoDB
- echo $PATH
- sudo mkdir -p /usr/local/mongodb
- cp -R /path/to/download/mongodb/bin /usr/local/mongodb
    + sudo chmod 777 /usr/local/mongodb
- ls -la /usr/local/mongodb/bin
- vi ~/.bashrc
    + a -> to insert in vim
    + export PATH="/usr/local/mongodb/bin:$PATH"
    + Shift + :wq
- sourcee ~/.bashrc
- echo $PATH
- mongod -> error /data/db not found
    + sudo mkdir -p /data/db
    + or run: mongod --dbpath ~/Documents/test-mongodb-data

- open MondoDB Compass -> paste a standalone connection string
    + mongodb://127.0.0.1:27017
    + Connect

- ports
    + mongoDB 27017
    + http 80
    + https ssl 443
    + mysql 3306


- Document Database
    + Collection
        + document
            + document: có thể k cùng cấu trúc fields như SQL
            + ví dụ:
                + document1: _id, name, image
                + document2: _id, test
            + ưu điểm linh hoạt
            + với những data như khoá học trên f8 giống nhau -> nên sử dụng mongoose để giúp tổ chức theo dạng object model, và quản lý fields chặt chẽ hơn

- Create Database



* format conversation code
- prettier
- lint-staged
- husky
```json
    "scripts": {
        "beautiful": "prettier --single-quote --trailing-comma all --write src/**/*.{js, json, scss}",
        "start": "nodemon --inspect src/index.js",
        "watch": "node-sass --watch src/resources/scss/app.scss src/public/css/app.css",
    },
    "lint-staged": {
        "src/**/*.{js, json, scss}": "prettier --single-quote --trailing-comma all --write"
    },
    "husky": {
        "hooks": {
            "pre-commit": "lint-staged"
        }
    }
```

```javascript
let camelCases = ['alphaBravoCharlieDelta', 'singaporeAirlines', 'thatLazyBrownFox'];
let longCamelCases = (varNames) => {
  let tooLong = 0;
  const maxLimit = 3;
  for (value of varNames) {
    const regrex = /(^[a-z]|[A-Z0-9])[a-z]*/g;
    const matches = value.match(regrex);
    if(matches.length > maxLimit) {
      tooLong++;
    }
  }
  return tooLong;
}

console.log('Hello, world!', longCamelCases(camelCases))
```

```javascript
const initialState = { result: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "add":
      return { result: state.result + action.payload };
    case "subtract":
      return { result: state.result - action.payload };
    default:
      throw new Error();
  }
}

function Calculator() {
  const [state, dispatch] = useReducer(reducer, initialState);
  const inputRef = useRef();
  // const [number, updateNumber] = useState("");
  // const handleNumberChange = (e) => updateNumber(Number(e.target.value));

  return (
    <>
      <div>Result: {state.result}</div>
      <button
        onClick={() =>
          dispatch({
            type: "subtract",
            payload: Number(inputRef.current.value) // number
          })
        }
      >
        -
      </button>
      <button
        onClick={() =>
          dispatch({ type: "add", payload: Number(inputRef.current.value) // number })
        }
      >
        +
      </button>
      <div>
        <input
          ref={inputRef}
          type="number"
        //   onFocus={() => inputRef.current.value = ""}
          // value={number}
          // onChange={handleNumberChange}
        />
      </div>
    </>
  );
}
```

```javascript
function LoginForm(props) {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState(null);

  return (
    <div>
      <input
        onChange={(event) => setUsername(event.target.value)}
        name="username"
      />
      <input
        onChange={(event) => setPassword(event.target.value)}
        name="password"
        type="password"
      />
      <button onClick={() => props.login(username, password)}>Login</button>
    </div>
  );
}
```

```javascript
const ThemeContext = createContext();
const Content = (props) => {
  const context = useContext(ThemeContext);
  return (
    <section className={`theme-${context.theme}`}>
      <span>Current theme: {context.theme}</span>
      <button onClick={props.switchTheme}>Switch Theme</button>
    </section>
  );
};

function Test() {
  const [theme, setTheme] = useState("dark");
  const switchTheme = () => {
    theme === "dark" ? setTheme("light") : setTheme("dark");
  };
  return (
    <ThemeContext.Provider value={{ theme }}>
      <Content switchTheme={switchTheme} />
    </ThemeContext.Provider>
  );
}
```

```javascript

const moveItem = (array, fromIndex, toIndex) =>
  array.reduce((prev, cur, idx, arr) => {
    if (idx === toIndex) prev.push(arr[fromIndex]);
    if (idx === fromIndex) return prev;
    prev.push(cur);
    return prev;
  }, []);

const List = (props) => {
  const [items, setItems] = useState(props.items);

  const handleClickItem = (item, index) => {
    // if only "B", uncomment check condition for "B"
    if (index === 0 /* || item !== "B" */) return;
    // items.splice(0, 0, items.splice(index, 1)[0]);
    // setItems([...items]);
    setItems(moveItem(items, index, 0));
  };

  return (
    <ul>
      {items.map((item, index) => {
        return (
          <li key={index} onClick={() => handleClickItem(item, index)}>
            {item}
          </li>
        );
      })}
    </ul>
  );
};
```

```typescript
class Book {
  constructor(private basePrice:number) {}

  finalPrice(): number {
      return this.basePrice * 2;
  }
}

class TaxableBook extends Book {
  constructor(basePrice:number, taxRate: number) {
    super(basePrice * taxRate);
  }
}

console.log(new TaxableBook(10, 2).finalPrice()); // 40
```

```javascript
const sampleOptions = [
  { id: "753", title: "This is the first option" },
  { id: "053", title: "This is the second option" }
];

class OptionsShower extends Component {
  constructor(props) {
    super(props);
    const { options } = props;
    this.state = { options, displayOptions: false };
    this.displayOptions = this.displayOptions.bind(this);
  }

  displayOptions() {
    this.setState(
      {
        options: this.state.options,
        displayOptions: !this.state.displayOptions
      },
      () => {
        console.log("this.state", this.state);
      }
    );
  }

  render() {
    return (
      <>
        <ul>
          {this.state.displayOptions &&
            this.state.options?.map((o) => <li key={o.id}>{o.title}</li>)}
        </ul>
        <button onClick={this.displayOptions}>
          {this.state.displayOptions ? "Hide" : "Show"}
        </button>
      </>
    );
  }
}
```

1 - 2.49  - 2.49
2 - 4.68  - 2.34
3 - 7.32  - 2.44
5 - 11.95 - 2.39

<!-- 2 + 3 = 4.68 + 7.32 = 12 -->
2 + 2 + 1 = 4.68 + 4.68 + 2.49 = 11.85

Còn câu 3