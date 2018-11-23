# moment

当前日期 moment().format('YYYY-MM-DD') // "2018-10-23"
最近7天  moment().subtract(7,'days').format('YYYY-MM-DD')  // "2018-10-16"
最近30天 moment().subtract(30,'days').format('YYYY-MM-DD') // "2018-09-23"

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

## 限制选择时间
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
