---
layout: post
title: "[React] inputs of Array useState 사용하기"
date: 2021-02-08 00:00:00 +0300
comments: true
description: useState 에서 inputs of Array 사용하는 방법
img: react.jpg 
visible: 1
categories: react
tags: [react]
---

## 1. input 태그의 value를 useState hook으로 관리하기
먼저 input 태그의 value를 useState hook을 통해 바인드해보겠습니다.

```tsx
import React, { useEffect, useState } from 'react';

function MyComponent() {
  const [inputValue, setInputValue] = useState('hello');
  return (
        <input value={inputValue}></input>
      );
    }


  export default MyComponent;
```

이렇게 value 값을 바인딩하면 input 태그의 value값을 수정할 수 없습니다. 왜냐하면 value값에 바인딩 되어있는 inputValue 값이 변하지 않기 때문인데요! 그렇기 때문에

### input 태그를 사용할 때에는 onChange 를 통해 바인드된 데이터를 변경해주어야 합니다!

input 값이 변경될 때(onChnage) 호출 할 함수를 onChnageValue라고 하고 생성해보겠습니다.

```tsx
import React, { useEffect, useState } from 'react';

function MyComponent() {
  const [inputValue, setInputValue] = useState('hello');
  const onChangeValue = (e:any):void => {
      setValue(e.target.value);
  }
  return (
        <input value={inputValue} onChange={onChangeValue}></input>
      );
    }


  export default MyComponent;
```

위와같이 onChnage 로 실행되는 함수에는 기본적으로 event 파라미터가 넘어오기 때문에 그녀석을 잡아서 value값을 inputValue에 저장하는 것입니다.

이렇게 되면 input의 value값이 변경됨에 따라서 inputValue값도 변경되는 것이죠!

## 2. inputs of Array를 useState hook으로 관리하기

그럼이번엔 useState에 obeject array를 세팅하고 순회하면서 input을 여러개 만들어보겠습니다.

```tsx
function MyComponent() {
  const [inputArray, setInputArray] = useState(
    [
      {name: 'kim', age: '16', comment: 'hello'},
      {name: 'lee', age: '20', comment: 'good day!'},
      {name: 'park', age: '16', comment: 'nice to meet you!'},
    ]
  );

  return (
        <>
        {inputArray.map((person)=> {
          return (
            <div>
                <ul>{person.name}</ul>
                <ul>{person.age}</ul>
                <input value={person.comment}></input>
            </div>
          )
        })}
        </>
  );
}
```

input value에 person의 comment를 집어넣었습니다. 마찬가지로 onChange 함수를 만들어줘야 값이 동적으로 바인딩 되게 만들 수 있습니다. 이때는 index를 이용해서 아래와 같이 바인딩할 수 있습니다.

```tsx
function MyComponent() {
  const [inputArray, setInputArray] = useState(
    [
      {name: 'kim', age: '16', comment: 'hello'},
      {name: 'lee', age: '20', comment: 'good day!'},
      {name: 'park', age: '16', comment: 'nice to meet you!'},
    ]
  );

  const onChangeValue = (e:any, index:number):void => {
    if (inputArray != undefined) {
      // 기존의 inputArray와 똑같은 배열을 하나 생성합니다.   
      let new_inputArray = [...inputArray];
      //그 배열의 알맞은 인덱스의 value값을 저장하고  
      new_inputArray[index].comment = e.target.value;
      // 새로운 배열을 통째로 setState 합니다.   
      setInputArray(new_inputArray);                 
    }
    
  }
  return (
        <>
        {/* map 메서드 callbackfn의 두번째 파라미터는 index이므로 이것을 이용합니다. */}
        {inputArray.map((person, index)=> {
          return (
            <div>
              <ul>{person.name}</ul>
              <ul>{person.age}</ul>
              {/* onChange에 onChangeValue를 실행하는 함수를 하나 만들어 index값을 같이 넘겨세요! */}
              <input value={person.comment} onChange={e => {onChangeValue(e, index)}}></input>
            </div>
          )
        })}
        </>
  );
}
```

setState를 할 때에는 배열의 특정요소만 변경할 수 없고(object라면 가능하지만) 배열을 통째로 변경해야합니다. 그렇기 때문에 기존과 똑같은 새로운 배열을 만들어 값을 수정한 후 통째로 변경하면 됩니다!

끝!