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
