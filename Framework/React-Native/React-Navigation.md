### 사용 이유

react native에서 화면 전환 기능을 사용하기 위해서는 navigation을 이용해야한다. router와 기능이 유사하지만 react native는 router를 사용하지 못하기 때문이다. react native에서 쓰이는 라우터의 종류가 여러가지 있으나, 그 중에서 가장 많이 쓰이는 것은 react navigation이다. react navigation은 공식 문서도 존재할 뿐만 아니라, 많은 사람들이 사용하고 있어 오류를 해결하기 수월하다.



### 원리

스택에 화면을 쌓아두어, 필요할 때 이 스택안에서 이동할 수 있다. 하지만, 스택 안에서 이동할 경우 이전 페이지를 유지할 수 있지만, 돌아갔을때, 화면을 reloading 하지 못하는 단점이 있다.



### 설치

```bash
yarn add react-navigation
npm install react-navigation
```

```bash
yarn add @react-navigation/native
npm install @react-navigation/native
```

```bash
yarn add react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
npm install react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
```



---

### Stack

```bash
yarn add @react-navigation/stack
npm install @react-navigation/stack
```

**createStackNavigator**

screen과 navigator 객체를 리턴

navigator는 screen을 자식 요소로 포함하고, 여러 screen을 자식 요소로 삼을 수 있음



**NavigationContainer**

navigator tree와 여러 navigation들을 포함

최상위 루트에 속하므로 주로 App.js에서 사용



### Navigator

```javascript
function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

**intialRouteName**

App.js를 reload하거나 screen에서 변화를 시도할 때, 지정해준 screen으로 이동



### Moving between screens

**방법**

`navigate`와 `push`를 이용

```javascript
navigation.navigate('Details');
navigation.push('Details');
```



**navigate vs push**

navigate는 먼저 동일한 route 객체가 있는지 확인해서 있으면 해당 route로 이동하고, 없으면 route를 스택에 새로 쌓음

push는 무조건 route를 스택에 새로 쌓음

∴ 지나온 루트를 순차적으로 기록하기 위해선 push를 쓰는 것이 나음



**※ navigate를 써서 무조건 스택에 넣으려면?**

```javascript
navigate({routeName: ‘MyRoute’, key: data.uniqueId, params: data});
```



**※스택 초기화하면서 스크린 이동하기**

```javascript
import {CommonActions} from '@react-navigation/native';
...
this.props.navigation.dispatch(
    CommonActions.reset({
        index: 1,
        routes: [{name: 'drawer'}],
    }),
);
```



### Dawer + Bottom + Toptab

구조: 스택(드로워(탭(스택)))

```javascript
// Tab
function TapNavigator() {
  return (
    <Tab.Navigator
      initialRouteName="기록"
      screenOptions={({route}) => ({
        tabBarIcon: ({focused, color, size}) => {
          let iconName;

          if (route.name === '커뮤니티') {
            iconName = focused ? 'earth' : 'earth-outline';
          } else if (route.name === '기록') {
            iconName = focused ? 'calendar' : 'calendar-outline';
          } else if (route.name === '추천') {
            iconName = focused ? 'medal' : 'medal-outline';
          } else {
            iconName = focused ? 'analytics' : 'analytics-outline';
          }

          // You can return any component that you like here!
          return <Icon name={iconName} size={size} color={color} />;
        },
      })}
      tabBarOptions={{
        activeTintColor: '#fff',
        inactiveTintColor: '#fad499',
        style: {
          backgroundColor: '#f39c12',
          paddingVertical: 5,
        },
        labelStyle: {
          fontSize: 15,
        },
      }}>
      <Tab.Screen name="기록" component={RecordStack} />
      <Tab.Screen name="커뮤니티" component={CommunityStack} />
      <Tab.Screen name="추천" component={RankStack} />
      <Tab.Screen name="분석" component={AnalysisScreen} />
    </Tab.Navigator>
  );
}

class DrawerStack extends Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <>
        <Drawer.Navigator
          initialRouteName="메뉴"
          drawerPosition="right"
          drawerContent={() => (
            <CustomDrawerContent navigation={this.props.navigation} />
          )}
          screenOptions={{
            headerShown: false,
          }}
          // drawerIcon={{foucsed: true, color: 'red', size: 20}}
          hideStatusBar={true}
          statusBarAnimation={true}>
          <Drawer.Screen name="메뉴" component={TapNavigator} />
          <Drawer.Screen name="내 정보" component={ProfileScreen} />
          <Drawer.Screen name="내 피드" component={FeedScreen} />
        </Drawer.Navigator>
      </>
    );
  }
}

const stackApp = createStackNavigator();
// export default function App() {
export default class App extends Component {
  constructor(props) {
    super(props);
  }
  componentDidMount() {
    SplashScreen.hide();
  }
  render() {
    return (
      <Provider store={store}>
        <NavigationContainer>
          <Stack.Navigator
            initialRouteName="로그인"
            screenOptions={{
              headerShown: false,
            }}>
            <stackApp.Screen name="로그인" component={AcccountStack} />
            <stackApp.Screen name="drawer" component={DrawerStack} />
          </Stack.Navigator>
        </NavigationContainer>
      </Provider>
    );
  }
}
```

