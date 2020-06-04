# CI tips

### CircleCI :: generate list failed tests
```JavaScript
let failed_tests = document.querySelectorAll('ul li')
let failed_tests_text = '';
let failed_tests_list = [];
failed_tests.forEach((item, index) => {
  let fail_el = item.querySelector('header > div');
  if (fail_el !== null) {
    let test_name = fail_el.textContent.split(' - ');
    failed_tests_list.push(test_name[1] + '.' + test_name[0]);
  }
})
failed_tests_list = failed_tests_list.sort()
failed_tests_list.forEach(element => failed_tests_text += element + "\n");
console.log(failed_tests_text);
```
