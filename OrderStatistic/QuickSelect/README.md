# Quick Select
<table>
    <tr>
        <table>
            <tr>
                <td><strong><i>Class</i></strong></td>
                <td><strong><i>Type</i></strong></td>
                <td><strong><i>Category</i></strong></td>
                <td><strong><i><a href="/DataStructures/">Data Structure</a></i></strong></td>
                <td><strong><i>Space</i></strong></td>
                <td><strong><i>Time: Worst</i></strong></td>
                <td><strong><i>Time: Average</i></strong></td>
            </tr>
            <tr>
                <td><a href="/OrderStatistic/">Order Statistic</a></td>
                <td>Randomized</td>
                <td>Efficient</td>
                <td>Array</td>
                <td><i>O</i>(log n)</td>
                <td><i>O</i>(n<sup>2</sup>)</td>
                <td><i>O</i>(n)</td>
            </tr>
        </table>
    </tr>
    <tr>
        <table>
            <tr style="text-align: center; font-size:20px;">
                <td><strong><i>GIF</i></strong></td>
                <td><strong><i>Video</i></strong></td>
            </tr>
            <tr>
                <td style="text-align: center;"><img src="QuickSelect.gif" alt="Quick Select GIF" style="width: auto; height: 315px;"/></td>
                <td style="text-align: center;"><a href="https://youtu.be/TlJhgPWM_Kc"><img src="http://img.youtube.com/vi/TlJhgPWM_Kc/0.jpg" alt="Quick Select Video" width="560" height="315"/></a></td>
            </tr>
        </table>
    </tr>
</table>

# Python Implementation
``` python
import random as r

def quick_select(ary, i): 
    
    def random_partition(start, end):
        k = r.randint(start, end)
        ary[end], ary[k], k = ary[k], ary[end], start - 1
        for j in range(start, end):
            if ary[j] <= ary[end]:
                ary[k+1], ary[j], k = ary[j], ary[k+1], k + 1
        ary[k+1], ary[end] = ary[end], ary[k+1]
        return k + 1
    
    def recurse(start, end, i):
        if start == end:
            return ary[start]
        mid = random_partition(start, end)
        k = mid - start + 1
        if i == k: return ary[mid]
        elif i < k: return recurse(start, mid - 1, i)
        return recurse(mid + 1, end, i - k)
    
    return recurse(0, len(ary) - 1, i)
```

# Java Implementation
``` java
import java.util.Random;

static int quick_select(int[] ary, int i) {
    return recurse(ary, 0, ary.length - 1, i);
}

static int recurse(int[] ary, int start, int end, int i) {
    if (start == end) {
        return ary[start];
    }
    int mid = random_partition(ary, start, end);
    int k = mid - start + 1;
    if (i == k) {
        return ary[mid];
    } else if (i < k) {
        return recurse(ary, start, mid - 1, i);
    }
    return recurse(ary, mid + 1, end, i - k);
}

static int random_partition(int[] ary, int start, int end) {
    int k = new Random().nextInt(end - start) + start, temp = ary[end];
    ary[end] = ary[k];
    ary[k] = temp;
    int x = ary[end], i = start - 1;
    for (int j = start; j < end; j++) {
        if (ary[j] <= x) {
            temp = ary[++i];
            ary[i] = ary[j];
            ary[j] = temp;
        }
    }
    temp = ary[i+1];
    ary[i+1] = ary[end];
    ary[end] = temp;
    return i + 1;
}
```