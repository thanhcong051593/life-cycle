# [Thực hành] Lifecyle react 16.3
## Mục tiêu
 - Hiểu được các hàm vòng đời của một React Component và các methods để quản lý vòng đời này
 - Bổ sung 3 life cycle mới.

## Mô tả
 - Tạo 2 component : App (component cha) và Content (Component con)
 - Component App chứa :  button INCREMENT và component Content
 - Component con Content nhận Props là myNumber, component này chứa các hàm lifeCycle, mỗi hàm sẽ chứa log hoặc alert thông báo tên hàm.
 - Chạy App và quan sát thứ tự các hàm được gọi tại 2 trường hợp, trả lời 2 câu hỏi sau
 - Lúc App khởi động những hàm nào được gọi ?
 - Khi click vào nút Increment hàm nào được gọi ?

 
## Hướng dẫn

   ***Bước 1:*** Tạo component App (component Cha) với code như sau:
   
    import React, { Component } from 'react';
    import {
      Platform,
      StyleSheet,
      Text,
      View, Button,
    } from 'react-native';
    import Content from './src/Content';
    type Props = {};
    
    export default class App extends Component<Props> {

     constructor(props) {
       super(props);
       this.state = { increment : 0 };
       this.increment = this.increment.bind(this);
     }

     increment() {
       this.setState({ increment: this.state.increment + 1 });
     }

     render() {
       return (
         <View style={styles.container}>
           <Button onPress={this.increment} title="INCREMENT" color="#841584" />
           <Content myNumber={this.state.increment} />
         </View>
       );
     }
    }


   Nội dung component App bao gồm 1 button và 1 component content giống như đề bài

   ***Bước 2:*** Tạo component <Content /> với nội dung bên dưới:
   
    import React, { Component } from 'react';
    import {
        Platform,
        StyleSheet,
        Text,
        View, Button, Alert,
    } from 'react-native';

    type Props = {};
    class Content extends Component<Props> {

       componentWillMount() {
           Alert.alert('componentWillMount');
       }
       componentDidMount() {
           Alert.alert('componentDidMount');
       }
       componentWillReceiveProps(newProps) {
           Alert.alert('componentWillReceiveProps');
       }
       shouldComponentUpdate(newProps, newState) {
           return true;
       }
       componentWillUpdate(nextProps, nextState) {
           Alert.alert('componentWillUpdate');
       }
       componentDidUpdate(prevProps, prevState) {
           Alert.alert('componentDidUpdate')
       }
       componentWillUnmount() {
           Alert.alert('componentWillUnmount')
       }
        static getDerivedStateFromProps(props, state){
        Alert.alert('getDerivedStateFromProps')
       }
       getSnapshotBeforeUpdate(prevProps, prevState){
         Alert.alert('getSnapshotBeforeUpdate')
       }
       componentDidCatch(error, info){
         Alert.alert('componentDidCatch')
       }
       render() {
           return (
               <View><Text>{this.props.myNumber}</Text></View>
           );
       }
    }
    export default Content

   Nhiệm vụ của component này : nhận Props từ ngoài vào, chứa các hàm lifeCycle.
   
   ***Bước 3:*** Chạy App để quan sát giao diện, chú ý các Alert hiện lên màn hình lần đầu tiên

   ***Bước 4:*** Tiếp tục click vào nút Increment và quan sát kết quả alert thông báo ra
   
   **Chú ý**: các life cycle: componentWillMount, componentWillReceiveProps, componentWillUpdate sẽ được bỏ ở version react 17
   

