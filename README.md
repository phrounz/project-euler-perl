# project-euler-perl
Some solutions for projecteuler.net in Perl. Most are dirty brute force ways, but hey.

## 1
```perl
my $sum = 0;
for (my $i = 0; $i < 1000; $i++) {
	if (($i % 3 == 0) || ($i % 5 == 0)) {
		$sum += $i;
	}
}
print "$sum\n";
```

## 2
```perl
my @l_fibocache;
sub fibo($) { 
	my $n = shift; 
	unless (exists $l_fibocache[$n]) {
		if    ($n == 0)  { $l_fibocache[$n] = 0 }
		elsif ($n == 1 ) { $l_fibocache[$n] = 1 }
		else             { $l_fibocache[$n] = fibo($n-1)+fibo($n-2) }
	}
	return $l_fibocache[$n];
}
my $sum = 0;
my $i = 0;
my $n = 0;
while ($n < 4000000) {
	$n = fibo($i);print "$n -> $sum\n";
	$sum += $n if ($n%2==0);
	$i++;
}
print "$sum\n";
```

## 3
```perl
my $n = 600851475143;
my $j = 0;
my $i = 3;
if ($n % 2 == 0) {
	$n /= 2;
}
while ($n > 1) {
	if ($n % $i == 0) {
		$n /= $i;
		print "$i\n";
	} else {
		$i+=2;
	}
}
```

## 4
```perl
use POSIX;
sub isPalindrom($) {
	my $str = "".shift()."";
	if (substr($str, 0,int(length($str)/2)) eq reverse(substr($str, POSIX::ceil(length($str)/2.0)))) {
		return 1;
	}
	return 0;
}
my $biggest = 0;
my $strinfo = "";
for (my $i = 100; $i < 1000; $i++) {
	for (my $j = 100; $j < 1000; $j++) {
		my $n = $i*$j;
		if (isPalindrom($n) && ($n > $biggest)) {
			$biggest = $n;
			$strinfo = "$i * $j";
		}
	}
}
print "$biggest $strinfo\n";
```

## 5
```perl
my $n = 2520;
while (1) {
	my $okdiv = 1;
	for (my $i = 20; $i > 1; $i--) {
		if ($n % $i != 0) {
			$okdiv = 0;
			last;
		}
	}
	if ($okdiv) { print "$n\n"; last } #  && ($n%2520==0)
	$n+=2520;
}
```

## 6 
```perl
my $sum_of_squares = 0;
my $sum = 0;
for (my $i = 1; $i <= 100; $i++) {
	$sum_of_squares += $i*$i;
	$sum += $i;
}
print $sum*$sum-$sum_of_squares;print " $sum*$sum-$sum_of_squares \n";
```

## 7
```perl
use Data::Dumper;
my @l_primecache = ( 2 );
my $n = 3;
my $i = 0;
while (scalar(@l_primecache) < 10001) {
	my $ok = 1;
	for (my $j = 0; $j < scalar(@l_primecache); $j++) {
		if ($n % $l_primecache[$j] == 0) { # $n can be divided by a prime number
			$ok = 0;
			last;
		}
	}
	if ($ok) { # new prime number
		push @l_primecache, $n;
	}
	$n+=2;
}
print Dumper(\@l_primecache);
```

## 8
```perl
$s='73167176531330624919225119674426574742355349194934
96983520312774506326239578318016984801869478851843
85861560789112949495459501737958331952853208805511
12540698747158523863050715693290963295227443043557
66896648950445244523161731856403098711121722383113
62229893423380308135336276614282806444486645238749
30358907296290491560440772390713810515859307960866
70172427121883998797908792274921901699720888093776
65727333001053367881220235421809751254540594752243
52584907711670556013604839586446706324415722155397
53697817977846174064955149290862569321978468622482
83972241375657056057490261407972968652414535100474
82166370484403199890008895243450658541227588666881
16427171479924442928230863465674813919123162824586
17866458359124566529476545682848912883142607690042
24219022671055626321111109370544217506941658960408
07198403850962455444362981230987879927244284909188
84580156166097919133875499200524063689912560717606
05886116467109405077541002256983155200055935729725
71636269561882670428252483600823257530420752963450'
;
$s=~s/\n//g;

my $best = 0;
for (my $i = 0; $i < length($s); $i++) {
	#my $c = substr($s,$i, 1);
	my $product = 1;
	for (my $j = 0; $j < 13; $j++) {
		$product *= int(substr($s,$i+$j, 1));
	}
	$best = $product if ($product > $best);
}

print "$best\n";
```
