# 순열, 중복 순열, 조합, 중복 조합
오늘 다시 개념을 정리하면서 구현 패턴을 재확인했다.

## 기본 개념 정리
- 순열
  - 순서가 중요하다.
  - 중복 없는 순열은 선택한 요소들이 모두 달라야 하며, 구현할 때는 보통 방문 여부 배열을 사용한다.
  - 중복 순열은 같은 원소를 여러 번 선택할 수 있다. 이 경우 방문 체크가 필요 없고, 모든 선택 단계에서 모든 후보를 순회한다.

- 조합
  - 순서는 상관없다.
  - 중복 없는 조합에서는 한 번 선택한 원소는 다시 선택하지 않으며, 보통 재귀 호출 시 다음 원소부터 선택하도록 인덱스를 조절한다.
  - 중복 조합에서는 같은 원소를 여러 번 선택할 수 있으나, 순서를 고려하지 않기 때문에 재귀 호출시 현재 인덱스 또는 그 이후의 원소들을 다시 선택하도록 설계한다.

## 경우의 수
- 중복 순열
  - 경우의 수 : n^r (n개의 원소 중에서 r개를 선택할 때, 매 선택마다 n가지 선택지가 있으므로)
- 순열
  - 경우의 수 : n!/(n-r)! (n개에서 순서를 고려하여 r개를 선택하는 경우)
- 중복 조합
  - 경우의 수 : (n + r - 1)!/(r! * (n + r - 1 - r))! => (n + r - 1)! / (r! × (n - 1)!) (원소를 중복해서 뽑는 동시에 순서는 고려하지 않는 경우)
- 조합
  - 경우의 수 : n!/r!(n-r)! (순서 없이 r개를 뽑는 경우)

## Java로 구현
- 중복 순열
```
void permutationWithRepetition(int depth, int r) {
    if (depth == r) {
        // 결과 처리
        return;
    }
    for (int i = 0; i < n; i++) {
        result[depth] = arr[i];
        permutationWithRepetition(depth + 1, r);
    }
}
```
- 순열
```
void permutationWithoutRepetition(int depth, int r, boolean[] visited) {
    if (depth == r) {
        // 결과 처리
        return;
    }
    for (int i = 0; i < n; i++) {
        if (visited[i]) continue;
        visited[i] = true;
        result[depth] = arr[i];
        permutationWithoutRepetition(depth + 1, r, visited);
        visited[i] = false;
    }
}
```
- 중복 조합
```
void combinationWithRepetition(int start, int depth, int r) {
    if (depth == r) {
        // 결과 처리
        return;
    }
    for (int i = start; i < n; i++) {
        result[depth] = arr[i];
        combinationWithRepetition(i, depth + 1, r);
    }
}
```
- 조합
```
void combinationWithoutRepetition(int start, int depth, int r) {
    if (depth == r) {
        // 결과 처리
        return;
    }
    for (int i = start; i < n; i++) {
        result[depth] = arr[i];
        combinationWithoutRepetition(i + 1, depth + 1, r);
    }
}
```

## 특징
- **순열 (중복/비중복)**: 모든 인덱스를 반복하며 방문 여부로 중복 제거
- **조합 (중복/비중복)**: 중복 제거를 위해 시작 인덱스를 고정하거나 유지
  - 비중복 조합: `i + 1`부터 반복 (다음 것부터만 선택)
  - 중복 조합: `i`부터 반복 (현재도 다시 선택 가능)
