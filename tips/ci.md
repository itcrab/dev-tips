# CI tips

### CircleCI :: parsing list failed tests
```JavaScript
// UPD: 2021-10-11
let failed_tests = document.querySelectorAll('ul li h4')
let failed_tests_text = '';
let failed_tests_list = [];
failed_tests.forEach((item, index) => {
  let test_name = item.textContent.split(' - ');
  failed_tests_list.push(test_name[1] + '.' + test_name[0]);
})
failed_tests_list = failed_tests_list.sort()
failed_tests_list.forEach(element => failed_tests_text += element + "\n");
console.log(failed_tests_text);
```
