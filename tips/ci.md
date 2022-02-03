# CI tips

### CircleCI :: parsing list failed tests
```JavaScript
// UPD: 2022-02-03
let failed_tests = document.querySelectorAll('ul li')
let failed_tests_text = '';
let failed_tests_list = [];
failed_tests.forEach((item, index) => {
  let test_name = item.querySelector('header > div:nth-child(2) h4')
  let test_path = item.querySelector('header > div:nth-child(2) > div:nth-child(2)')
  if (test_name !== null && test_path !== null) {
    failed_tests_list.push(test_path.textContent + '.' + test_name.textContent);
  }
})
failed_tests_list = failed_tests_list.sort()
failed_tests_list.forEach(element => failed_tests_text += element + "\n");
console.log(failed_tests_text);
```
