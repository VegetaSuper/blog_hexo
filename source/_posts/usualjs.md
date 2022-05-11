---
title: 常用的JS函数
tags:
  - JavaScript
categories:
  - 开发
  - 常用方法
date: 2022-05-09 15:45:38
cover: http://rblypd9jp.bkt.clouddn.com/picture/js1.jpg
---

# 记录开发中常用的方法(一)

## 将扁平数据转换为树结构

```javascript
/**
 * @param {*} arrary 扁平数据
 * @param {*} key 主键
 * @param {*} parent_key // 父级主键
 * @param {*} root // 根节点
 * @returns
 */
function arrayToTree(arrary, key = 'id', parent_key = 'pid', root = 0) {
  const result = [] // 存放结果
  const itemMap = {}
  for (const item of arrary) {
    const id = item[key]
    const pid = item[parent_key]

    if (!itemMap[id]) {
      itemMap[id] = {
        children: [],
      }
    }

    itemMap[id] = {
      ...item,
      children: itemMap[id]['children'],
    }

    const treeItem = itemMap[id]

    if (pid === root) {
      result.push(treeItem)
    } else {
      if (!itemMap[pid]) {
        itemMap[pid] = {
          children: [],
        }
      }
      itemMap[pid].children.push(treeItem)
    }
  }
  return result
}
```

## 深拷贝

```javascript
/**
 * @param {*} origin 原数据
 * @param {} target 深拷贝后
 * @returns
 */
function deepClone(origin, target = {}) {
  var toStr = Object.prototype.toString,
    arrAtr = '[object Array]'
  for (var prop in origin) {
    //遍历对象
    if (origin.hasOwnProperty(prop)) {
      //防止拿到原型链属性
      if (origin[prop] !== 'null' && typeof origin[prop] == 'object') {
        //判断是不是原始值
        target[prop] = toStr.call(origin[prop]) == arrAtr ? [] : {} // 建立相对应的数组或对象
        myDeepClone(origin[prop], target[prop]) // 递归，为了拿到引用值里面还有引用值
      } else {
        target[prop] = origin[prop] // 原始值，直接拷贝
      }
    }
  }
  return target
}
```

## 将字符串转为 base64

```javascript
function base64Encode(data) {
  var toBase64Table =
    'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
  var base64Pad = '='
  var result = ''
  var length = data.length
  var i
  // Convert every three bytes to 4 ascii characters.

  for (i = 0; i < length - 2; i += 3) {
    result += toBase64Table[data.charCodeAt(i) >> 2]
    result +=
      toBase64Table[
        ((data.charCodeAt(i) & 0x03) << 4) + (data.charCodeAt(i + 1) >> 4)
      ]
    result +=
      toBase64Table[
        ((data.charCodeAt(i + 1) & 0x0f) << 2) + (data.charCodeAt(i + 2) >> 6)
      ]
    result += toBase64Table[data.charCodeAt(i + 2) & 0x3f]
  }

  // Convert the remaining 1 or 2 bytes, pad out to 4 characters.

  if (length % 3) {
    i = length - (length % 3)
    result += toBase64Table[data.charCodeAt(i) >> 2]
    if (length % 3 == 2) {
      result +=
        toBase64Table[
          ((data.charCodeAt(i) & 0x03) << 4) + (data.charCodeAt(i + 1) >> 4)
        ]
      result += toBase64Table[(data.charCodeAt(i + 1) & 0x0f) << 2]
      result += base64Pad
    } else {
      result += toBase64Table[(data.charCodeAt(i) & 0x03) << 4]
      result += base64Pad + base64Pad
    }
  }
  return result
}
```

## 解析 base64

```javascript
function base64Encode(data) {
  /** Convert Base64 data to a string */
  var toBinaryTable = [
    -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
    -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
    -1, -1, -1, -1, -1, 62, -1, -1, -1, 63, 52, 53, 54, 55, 56, 57, 58, 59, 60,
    61, -1, -1, -1, 0, -1, -1, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13,
    14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, -1, -1, -1, -1, -1, -1, 26,
    27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45,
    46, 47, 48, 49, 50, 51, -1, -1, -1, -1, -1,
  ]
  var result = ''
  var leftbits = 0
  var leftdata = 0
  for (var i = 0; i < data.length; i++) {
    var c = toBinaryTable[data.charCodeAt(i) & 0x7f]
    var padding = data.charCodeAt(i) == '='.charCodeAt(0)
    if (c == -1) continue
    leftdata = (leftdata << 6) | c
    leftbits += 6
    if (leftbits >= 8) {
      leftbits -= 8
      if (!padding) result += String.fromCharCode((leftdata >> leftbits) & 0xff)
      leftdata &= (1 << leftbits) - 1
    }
  }
  if (leftbits) throw Components.Exception('Corrupted base64 string')
  return result
}
```

## 合并区间

```javascript
/**
 * 合并区间
 * @param {number[][]} intervals
 * @return {number[][]}
 */
function merge(intervals) {
  // 如果传递进来的数组长度为0 返回一个空数组
  if (intervals.length === 0) return []
  // 创建合并数组
  var res = []
  // 将数组进行升序排序
  intervals.sort(function (a, b) {
    return a[0] - b[0]
  })
  // 结果数组放进第一个数组
  res.push(intervals[0])
  // 从原数组的第一个元素进行遍历
  for (var i = 1; i < intervals.length; i++) {
    // 如果当前区间的左端点 大于 merge数组最后一个元素的右端点
    if (intervals[i][0] > res[res.length - 1][1]) {
      // 说明这个数组可以直接放进merge数组中
      res.push(intervals[i])
    } else {
      // 说明有区间有交集 当前区间的左端点小于等于最后一个元素的右端点
      // 如果当前区间的右端点 大于 merge 最后一个右端点
      if (intervals[i][1] > res[res.length - 1][1]) {
        // 更新右端点为最大值
        res[res.length - 1][1] = intervals[i][1]
      }
    }
  }
  return res
}
```

## 判断是否是图片文件

```javascript
function IsPicture(fileName) {
  var strFilter = '.jpeg|.gif|.jpg|.png|.bmp|.pic|.svg|'
  if (fileName.indexOf('.') > -1) {
    var p = fileName.lastIndexOf('.')
    var strPostfix = fileName.substring(p, fileName.length) + '|'
    strPostfix = strPostfix.toLowerCase()
    if (strFilter.indexOf(strPostfix) > -1) {
      return true
    }
  }
  return false
}
```

## 判断是否是音频文件

```javascript
function IsVoice(fileName) {
  var strFilter = '.mpeg|.rm|.ram|.swf|.mp3|.wma|.rm|'
  if (fileName.indexOf('.') > -1) {
    var p = fileName.lastIndexOf('.')
    var strPostfix = fileName.substring(p, fileName.length) + '|'
    strPostfix = strPostfix.toLowerCase()
    if (strFilter.indexOf(strPostfix) > -1) {
      return true
    }
  }
  return false
}
```

## 判断是否是视频文件

```javascript
function IsVideo(fileName) {
  var strFilter = '.mp4|.m2v|.mkv|.rmvb|.wmv|.avi|.flv|.mov|.m4v|.mpg|'
  if (fileName.indexOf('.') > -1) {
    var p = fileName.lastIndexOf('.')
    var strPostfix = fileName.substring(p, fileName.length) + '|'
    strPostfix = strPostfix.toLowerCase()
    if (strFilter.indexOf(strPostfix) > -1) {
      return true
    }
  }
  return false
}
```
