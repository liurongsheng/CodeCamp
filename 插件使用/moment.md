# moment

当前日期 moment().format('YYYY-MM-DD') // "2018-12-05"
往前7天  moment().subtract(7,'days').format('YYYY-MM-DD')  // "2018-11-28"
往前30天 moment().subtract(30,'days').format('YYYY-MM-DD') // "2018-11-05"
往后7天  moment().add(7,'days').format('YYYY-MM-DD')  // "2018-12-12"
往后30天 moment().add(30,'days').format('YYYY-MM-DD') // "2019-01-04"

往前一个月 moment().subtract(1,'months').format('YYYY-MM-DD') // "2018-11-05"
往后一个月 moment().add(1,'months').format('YYYY-MM-DD') // "2019-01-05"

```
import moment from 'moment';
const { RangePicker } = DatePicker;
const dateFormat = 'YYYY-MM-DD';

let day = moment();
let dayBeforeWeek = moment().subtract(7,'days');
let dayBeforeMonth = moment().subtract(30,'days');

<Col span={8}>
  <span>交易日期：</span>
  <RangePicker
    onChange={dates => {
      this.setSearch({startTime: dates[0], endTime: dates[1]})
    }}
    defaultValue={[moment(dayBeforeWeek, dateFormat), moment(day, dateFormat)]}
    format={dateFormat}
  />
</Col>
```

## 下拉限制选择时间
```
disabledDate = (current) => {
  return current && current > moment.max(moment().subtract(1, 'day')); // 限制选择前一天的日期
  // return current && current > moment.max(moment().add(1, 'd')); // 限制选择后一天的日期
  // return current && current > moment().endOf('day'); // 限制选择今天和今天之前的日期
  // return current && current < moment().endOf('day'); // 限制选择今天之后的日期
};

<Col span={12}>
  账单日期：
  <RangePicker
    disabledDate={this.disabledDate}
    onChange={dates=>{this.fromDate=dates[0];this.toDate=dates[1];}}
    format="YYYY-MM-DD"
    placeholder={['开始时间', '结束时间']}
  />
</Col>
```

## 时间最大选择区间为当前时间往后一个月
```
<Col span={8} className="align-left">
  <span className="span-style">结算日期：</span>
  <RangePicker
    onChange={dates => {
      if(dates[0]){
        let start = moment(JSON.parse(JSON.stringify(dates[0]))) ;
        let nextMonth = start.add(1,'months').valueOf();
        if(dates[1].valueOf()>nextMonth){
          dates[1] = moment(nextMonth);
        }
      }
      this.setSearch({creationFromTime: dates[0], creationToTime: dates[1]})
    }}
    format="YYYY-MM-DD"
    className="align-left"
    placeholder={['开始时间', '结束时间']}
  />
</Col>
```

## 日期时间戳互转
日期转时间戳
`moment('2018-11-28 15:00:00', 'YYYY-MM-DD HH:mm:ss').valueOf();`

new Date('2018-11-28').valueOf()

时间戳转日期
`moment('1543363200000').format('YYYY-MM-DD HH:mm:ss');`
