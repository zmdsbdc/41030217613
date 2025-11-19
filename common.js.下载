// 对Date的扩展，将 Date 转化为指定格式的String
// 月(M)、日(d)、小时(h)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符， 
// 年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字) 
// 例子： 
// (new Date()).Format("yyyy-MM-dd hh:mm:ss.S") ==> 2006-07-02 08:09:04.423 
// (new Date()).Format("yyyy-M-d h:m:s.S")      ==> 2006-7-2 8:9:4.18 
Date.prototype.Format = function (fmt) { //author: meizz 
    var o = {
        "M+": this.getMonth() + 1, //月份 
        "d+": this.getDate(), //日 
        "h+": this.getHours(), //小时 
        "m+": this.getMinutes(), //分 
        "s+": this.getSeconds(), //秒 
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度 
        "S": this.getMilliseconds() //毫秒 
    };
    if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o)
        if (new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
}

Array.prototype.contains = function (obj) {
    var i = this.length;
    while (i--) {
        if (this[i] === obj) {
            return true;
        }
    }
    return false;
}

//获取url参数
$.params = function(name, url){
    if (!url) {
        url = window.location.href;
    }
    name = name.replace(/[\[\]]/g, "\\$&");
    var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
        results = regex.exec(url);
    if (!results) return /*null*/'';
    if (!results[2]) return '';
    return decodeURIComponent(results[2].replace(/\+/g, " "));
};

//替换url参数值
$.replaceParamVal = function(paramName, replaceWith, url){
    if (!url) {
        url = window.location.href;
    }
    var re = eval('/(' + paramName + '=)([^&]*)/gi');
    var nUrl = url.replace(re, paramName + '=' + replaceWith);
    return nUrl;
};

//将秒转换为时分秒
$.seconds2Hms = function (seconds) {
    var hours = Math.floor(seconds / 60 / 60);
    var minutes = Math.floor((seconds - hours * 60 * 60) / 60);
    seconds = seconds - hours * 60 * 60 - minutes * 60;
    var str = '';
    if (hours > 0) {
        str += hours + '小时';
    }
    if (minutes > 0) {
        str += minutes + '分';
    }
    else if (str != '') {
        str += minutes + '分';
    }
    str += seconds + '秒';
    return str;
}
//微信jsapi需要使用的JS接口列表
$.jsApiList = [
        'checkJsApi',
        'onMenuShareTimeline',
        'onMenuShareAppMessage',
        'onMenuShareQQ',
        'onMenuShareWeibo',
        'onMenuShareQZone',
        'hideMenuItems',
        'showMenuItems',
        'hideAllNonBaseMenuItem',
        'showAllNonBaseMenuItem',
        'translateVoice',
        'startRecord',
        'stopRecord',
        'onVoiceRecordEnd',
        'playVoice',
        'onVoicePlayEnd',
        'pauseVoice',
        'stopVoice',
        'uploadVoice',
        'downloadVoice',
        'chooseImage',
        'previewImage',
        'uploadImage',
        'downloadImage',
        'getNetworkType',
        'openLocation',
        'getLocation',
        'hideOptionMenu',
        'showOptionMenu',
        'closeWindow',
        'scanQRCode',
        'chooseWXPay',
        'openProductSpecificView',
        'addCard',
        'chooseCard',
        'openCard'
];

//url增加参数
$.addQueryString = function (url, queryString) {
    if (queryString) {
        if (url.indexOf('?') > -1) {
            url += "&" + queryString;
        }
        else {
            url += "?" + queryString;
        }
    }
    return url;
};

//生成guid
$.guid = function () {
    var S4 = function () {
        return (((1 + Math.random()) * 0x10000) | 0).toString(16).substring(1);
    };
    return (S4() + S4() + "" + S4() + "" + S4() + "" + S4() + "" + S4() + S4() + S4()).toUpperCase();
};

/////hours为空字符串时,cookie的生存期至浏览器会话结束。hours为数字0时,建立的是一个失效的cookie,这个cookie会覆盖已经建立过的同名、同path的cookie（如果这个cookie存在）。
function setCookie(name, value, hours, path) {
    var name = escape(name);
    var value = escape(value);
    var expires = new Date();
    expires.setTime(expires.getTime() + hours * 3600000);
    path = path == "" ? "" : ";path=" + path;
    _expires = (typeof hours) == "string" ? "" : ";expires=" + expires.toUTCString();
    document.cookie = name + "=" + value + _expires + path;
}

//获取cookie值
function getCookieValue(name) {
    var name = escape(name);
    //读cookie属性，这将返回文档的所有cookie
    var allcookies = document.cookie;
    //查找名为name的cookie的开始位置
    name += "=";
    var pos = allcookies.indexOf(name);
    //如果找到了具有该名字的cookie，那么提取并使用它的值
    if (pos != -1) {                                             //如果pos值为-1则说明搜索"version="失败
        var start = pos + name.length;                  //cookie值开始的位置
        var end = allcookies.indexOf(";", start);        //从cookie值开始的位置起搜索第一个";"的位置,即cookie值结尾的位置
        if (end == -1) {
            end = allcookies.length;
        }         //如果end值为-1说明cookie列表里只有一个cookie
        var value = allcookies.substring(start, end); //提取cookie的值
        return (value);                           //对它解码
    }
    else {
        return ""; //搜索失败，返回空字符串
    }
}

//删除cookie
function deleteCookie(name, path) {
    var name = escape(name);
    var expires = new Date(0);
    path = path == "" ? "" : ";path=" + path;
    document.cookie = name + "=" + ";expires=" + expires.toUTCString() + path;
}

//对列
var Queue=function() {

    //初始化队列（使用数组实现）
    var items = [];

    //向队列（尾部）中插入元素
    this.enqueue = function (element) {
        items.push(element);
    }

    //从队列（头部）中弹出一个元素，并返回该元素
    this.dequeue = function () {
        return items.shift();
    }

    //查看队列最前面的元素（数组中索引为0的元素）
    this.front = function () {
        return items[0];
    }

    //查看队列是否为空，如果为空，返回true；否则返回false
    this.isEmpty = function () {
        return items.length == 0;
    }

    //查看队列的长度
    this.size = function () {
        return items.length;
    }

    //查看队列
    this.print = function () {
        //以字符串形势返回
        return items.toString();
    }
}

// the code of these two functions is from mootools 
// http://mootools.net 
var $specialChars = { '\b': '\\b', '\t': '\\t', '\n': '\\n', '\f': '\\f', '\r': '\\r', '"': '\\"', '\\': '\\\\' };
var $replaceChars = function (chr) {
    return $specialChars[chr] || '\\u00' + Math.floor(chr.charCodeAt() / 16).toString(16) + (chr.charCodeAt() % 16).toString(16);
};

$.toJSON = function (o) {
    var s = [];
    switch ($.type(o)) {
        case 'undefined':
            return 'undefined';
        case 'null':
            return 'null';
        case 'number':
            return isFinite(o) ? String(o) : "null";
        case 'boolean':
            return o;
        case 'date':
            return '"/Date(' + o.getTime() + ')/"';
        case 'function':
            return o.toString();
        case 'string':
            if (o.indexOf("/Date(") > -1) {
                var d = eval("new " + o.substring(1, o.length - 1));
                return '"' + d.getFullYear() + "-" + (d.getMonth() + 1) + "-" + d.getDate() + '"';
            }
            return '"' + o.replace(/[\x00-\x1f\\"]/g, $replaceChars) + '"';
        case 'array':
            for (var i = 0, l = o.length; i < l; i++) {
                s.push($.toJSON(o[i]));
            }
            return '[' + s.join(',') + ']';
        case 'error':
        case 'object':
            for (var p in o) {
                if (p.substring(0, 1) == "_") {
                    s.push('\"' + p + '\":' + $.toJSON(o[p]));
                } else {
                    s.push('' + p + ':' + $.toJSON(o[p]));
                }
            }
            return '{' + s.join(',') + '}';
        default:
            return '';
    }
};

$.evalJSON = function (s) {
    if ($.type(s) != 'string' || !s.length) return null;
    return eval('(' + s + ')');
};

/*
    *  验证占比
    *  0：正确 -1：占比不满百分百 -2：占比超过百分百 -3 占比值存在非法表达方式 -4 传入参数错误
    */
$.CheckShareSum = function (arr) {
    var result = 0;
    if (arr == null || arr == undefined || Object.prototype.toString.call(arr) != '[object Array]') {
        result = -4
    }
    if (result == 0 && arr.length > 0) {

        var reg0 = /^((\d+\.?\d*)|(\d*\.\d+))\%$/;// 百分比
        var reg1 = /^[1-9]\d*\/[1-9]\d*$/;
        if (arr[0].match(reg0)) {
            var sum = 0;
            for (var i = 0, j = arr.length; i < j; i++) {
                if (arr[i].match(reg0)) {
                    sum += parseFloat(arr[i].replace(/\%$/g, ""));
                }
                else {
                    result = -3;
                    break;
                }
            }
            if (result == 0 && sum < 100) {
                result = -1;
            } else if (result == 0 && sum > 100) {
                result = -2;
            }

        } else if (arr[0].match(reg1)) {
            var parent = 1;
            for (var i = 0, j = arr.length; i < j; i++) {
                if (arr[i].match(reg1)) {
                    parent *= parseInt(arr[i].split("\/")[1]);
                }
                else {
                    result = -3;
                    break;
                }
            }
            if (result == 0) {
                var child = 0;
                for (var i = 0, j = arr.length; i < j; i++) {
                    child += parseInt(arr[i].split("\/")[0]) * parent / parseInt(arr[i].split("\/")[1]);

                }
                if (child < parent) {
                    result = -1;
                } else if (child > parent) {
                    result = -2;
                }

            }

        } else {
            result = -3;
        }
    }
    return result;
}
//下载文件
function downloadFile(url) {
    try {
        var elemIF = document.createElement("iframe");
        elemIF.src = url;
        elemIF.style.display = "none";
        document.body.appendChild(elemIF);
    } catch (e) {

    }
}
//获取滚动条高度
function getScrollTop() {
    var scroll_top = 0;
    if (document.documentElement && document.documentElement.scrollTop) {
        scroll_top = document.documentElement.scrollTop;
    }
    else if (document.body) {
        scroll_top = document.body.scrollTop;
    }
    return scroll_top;
}
//html编解码
function htmlencode(s) {
    var div = document.createElement('div');
    div.appendChild(document.createTextNode(s));
    return div.innerHTML;
}
function htmldecode(s) {
    var div = document.createElement('div');
    div.innerHTML = s;
    return div.innerText || div.textContent;
}
/**
 *获取GUID
 */
function Guid() {
    return 'xxxxxxxxxxxx4xxxyxxxxxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
        var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
}
/**
 * 金额正则
 * @param {any} obj
 */
var num = function (obj) {
    obj.value = obj.value.replace(/[^\d.]/g, ""); //清除"数字"和"."以外的字符
    obj.value = obj.value.replace(/^\./g, ""); //验证第一个字符是数字
    obj.value = obj.value.replace(/\.{2,}/g, "."); //只保留第一个, 清除多余的
    obj.value = obj.value.replace(".", "$#$").replace(/\./g, "").replace("$#$", ".");
    obj.value = obj.value.replace(/^(\-)*(\d+)\.(\d\d).*$/, '$1$2.$3'); //只能输入两个小数
}
function getTimeNumStr(num) {
    if (num < 10)
        return '0' + num;
    else
        return '' + num;
}
//展示格式化时间
function getTimeFormatF(str, fType) {
    if (!str || str.length <= 10)
        return str;
    if (str.indexOf("Date(") >= 0) {
        str = str.replace("/Date(", "").replace(")/", "");
        var dt = new Date(parseInt(str));
        str = dt.getFullYear() + "-" + getTimeNumStr(dt.getMonth() + 1) + "-" + getTimeNumStr(dt.getDate()) + " " + getTimeNumStr(dt.getHours()) + ":" + getTimeNumStr(dt.getMinutes()) + ":" + getTimeNumStr(dt.getSeconds());
    }
    if (fType != null && fType == 1) {
        var tmpstr = str.substring(0, 10).replace("-", "年").replace("-", "月");
        if (tmpstr.indexOf("日") < 0)
            tmpstr = tmpstr + "日";
        tmpstr = tmpstr + " ";
        return tmpstr;
    } else if (fType != null && fType == 2) {
        var tmpstr = str.substring(0, 10);
        tmpstr = tmpstr + " ";
        return tmpstr;
    } else if (fType != null && fType == 3) {
        return str;
    }
    return str.substring(0, 10);
}

//长度限制
function lengthLimit(obj, length) {
    var val = obj.value, str = "", l = 0;
    if (val) {
        if (val.replace(/[^\x00-\xff]/g, "xx").length <= length) {
            str = obj.value;
        } else {
            for (var i = 0; schar = val.charAt(i); i++) {
                str += schar;
                l += (schar.match(/[^\x00-\xff]/) != null ? 2 : 1);
                if (l >= length) {
                    break;
                }
            } 
        }
    } 
    obj.value=str;
}


function ValCardNo(carno) {
    var p = /^[1-9]\d{5}(18|19|20)\d{2}((0[1-9])|(1[0-2]))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/;
    return p.test(carno);
}

$.Validator = {

    /**
     * 手机号验证
     * @param {string} phone 手机号码
     * @returns {boolean} 验证结果
     */
    isValidPhone: function (phone) {
        if (!phone || typeof phone !== 'string') return false;

        // 中国大陆手机号正则（支持最新号段）
        var phoneRegex = /^1[3-9]\d{9}$/;
        return phoneRegex.test(phone.replace(/\s+/g, ''));
    },

    /**
     * 身份证号验证（18位）
     * @param {string} idCard 身份证号
     * @returns {boolean} 验证结果
     */
    isValidIdCard: function (idCard) {
        if (!idCard || typeof idCard !== 'string') return false;

        idCard = idCard.toUpperCase().replace(/\s+/g, '');

        // 18位身份证号正则
        var idCardRegex = /^[1-9]\d{5}(19|20)\d{2}(0[1-9]|1[0-2])(0[1-9]|[12]\d|3[01])\d{3}[0-9X]$/;

        if (!idCardRegex.test(idCard)) return false;

        // 验证校验码
        return this._validateIdCardChecksum(idCard);
    },

    /**
     * 身份证校验码验证
     * @param {string} idCard 18位身份证号
     * @returns {boolean} 校验码是否正确
     */
    _validateIdCardChecksum: function (idCard) {
        var weights = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];
        var checkCodes = ['1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2'];

        var sum = 0;
        for (var i = 0; i < 17; i++) {
            sum += parseInt(idCard.charAt(i)) * weights[i];
        }

        var checkCode = checkCodes[sum % 11];
        return checkCode === idCard.charAt(17);
    },

    /**
     * 邮箱验证
     * @param {string} email 邮箱地址
     * @returns {boolean} 验证结果
     */
    isValidEmail: function (email) {
        if (!email || typeof email !== 'string') return false;

        var emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
        return emailRegex.test(email.trim());
    },

    /**
     * 座机号验证
     * @param {string} tel 座机号码
     * @returns {boolean} 验证结果
     */
    isValidTelephone: function (tel) {
        if (!tel || typeof tel !== 'string') return false;

        // 支持格式：010-12345678、0571-87654321、400-123-4567等
        var telRegex = /^(0\d{2,3}-?)?\d{7,8}$|^400-?\d{3}-?\d{4}$/;
        return telRegex.test(tel.replace(/\s+/g, ''));
    },

    /**
     * 邮政编码验证
     * @param {string} zipCode 邮政编码
     * @returns {boolean} 验证结果
     */
    isValidZipCode: function (zipCode) {
        if (!zipCode || typeof zipCode !== 'string') return false;

        var zipRegex = /^[1-9]\d{5}$/;
        return zipRegex.test(zipCode.replace(/\s+/g, ''));
    },

    /**
     * 银行卡号验证
     * @param {string} bankCard 银行卡号
     * @returns {boolean} 验证结果
     */
    isValidBankCard: function (bankCard) {
        if (!bankCard || typeof bankCard !== 'string') return false;

        bankCard = bankCard.replace(/\s+/g, '');

        // 银行卡号长度一般为16-19位
        if (!/^\d{16,19}$/.test(bankCard)) return false;

        // Luhn算法验证
        return this._luhnCheck(bankCard);
    },

    /**
     * Luhn算法校验
     * @param {string} num 数字字符串
     * @returns {boolean} 校验结果
     */
    _luhnCheck: function (num) {
        var sum = 0;
        var alternate = false;

        for (var i = num.length - 1; i >= 0; i--) {
            var n = parseInt(num.charAt(i), 10);

            if (alternate) {
                n *= 2;
                if (n > 9) {
                    n = (n % 10) + 1;
                }
            }

            sum += n;
            alternate = !alternate;
        }

        return (sum % 10) === 0;
    },

    /**
     * 中文姓名验证
     * @param {string} name 姓名
     * @returns {boolean} 验证结果
     */
    isValidChineseName: function (name) {
        if (!name || typeof name !== 'string') return false;

        // 中文姓名正则，支持2-4个汉字，包含少数民族姓名中的·
        var nameRegex = /^[\u4e00-\u9fa5]{2,4}$|^[\u4e00-\u9fa5]{2,3}·[\u4e00-\u9fa5]{2,3}$/;
        return nameRegex.test(name.trim());
    },

    /**
     * 密码强度验证
     * @param {string} password 密码
     * @param {number} level 强度等级 1-简单 2-中等 3-复杂
     * @returns {boolean} 验证结果
     */
    isValidPassword: function (password, level) {
        if (!password || typeof password !== 'string') return false;

        level = level || 2;

        switch (level) {
            case 1: // 简单：至少6位数字或字母
                return /^[a-zA-Z0-9]{6,}$/.test(password);
            case 2: // 中等：至少8位，包含数字和字母
                return /^(?=.*[a-zA-Z])(?=.*\d)[a-zA-Z\d]{8,}$/.test(password);
            case 3: // 复杂：至少8位，包含大小写字母、数字和特殊字符
                return /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/.test(password);
            default:
                return false;
        }
    },

    /**
     * URL验证
     * @param {string} url URL地址
     * @returns {boolean} 验证结果
     */
    isValidUrl: function (url) {
        if (!url || typeof url !== 'string') return false;

        var urlRegex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
        return urlRegex.test(url.trim());
    },

    /**
     * 统一社会信用代码验证
     * @param {string} creditCode 统一社会信用代码
     * @returns {boolean} 验证结果
     */
    isValidCreditCode: function (creditCode) {
        if (!creditCode || typeof creditCode !== 'string') return false;

        creditCode = creditCode.toUpperCase().replace(/\s+/g, '');

        // 18位统一社会信用代码正则
        var creditRegex = /^[0-9A-HJ-NPQRTUWXY]{2}\d{6}[0-9A-HJ-NPQRTUWXY]{10}$/;

        if (!creditRegex.test(creditCode)) return false;

        // 验证校验码
        return this._validateCreditCodeChecksum(creditCode);
    },

    /**
     * 统一社会信用代码校验码验证
     * @param {string} creditCode 18位统一社会信用代码
     * @returns {boolean} 校验码是否正确
     */
    _validateCreditCodeChecksum: function (creditCode) {
        var weights = [1, 3, 9, 27, 19, 26, 16, 17, 20, 29, 25, 13, 8, 24, 10, 30, 28];
        var codes = '0123456789ABCDEFGHJKLMNPQRTUWXY';
        var codeMap = {};

        for (var i = 0; i < codes.length; i++) {
            codeMap[codes.charAt(i)] = i;
        }

        var sum = 0;
        for (var j = 0; j < 17; j++) {
            sum += codeMap[creditCode.charAt(j)] * weights[j];
        }

        var checkCode = 31 - (sum % 31);
        if (checkCode === 31) checkCode = 0;

        return codes.charAt(checkCode) === creditCode.charAt(17);
    }
};


/**
 * jQuery 验证插件
 * 包含手机号、身份证、邮箱等常用验证方法
 * 版本: 1.0.0
 * 日期: 2024-03-15
 */

 
 