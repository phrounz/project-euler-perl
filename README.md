# project-euler-perl
Some solutions for projecteuler.net in Perl. Most are dashed off dirty brute force solutions, but hey.

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


## 9
```perl

for (my $c = 1000-2; $c>=2; $c--) {
	for (my $b = $c-1; $b>=1; $b--) {
		my $a = 1000 - $b - $c;
		if ($a*$a + $b*$b == $c*$c) {
			print "$a $b $c product=".($a*$b*$c)."\n";
		}
	}
}

```

## 10
```perl
sub isPrime($) { 
	my $i = shift;
	for (my $j = 3; $j<= sqrt($i); $j++) {
		return 0 if ($i % $j == 0);
	}
	return 1;
}

my $sum = 2+3+5+7;
for (my $i = 11; $i < 2000000;$i+=2) {
	print "... $i\n" if ($i%10001==0);
	if (isPrime($i)) {
		$sum += $i;
	}
}
print "=> $sum\n";
```

## 11
```perl

#!/usr/bin/perl

my $data = "08 02 22 97 38 15 00 40 00 75 04 05 07 78 52 12 50 77 91 08
49 49 99 40 17 81 18 57 60 87 17 40 98 43 69 48 04 56 62 00
81 49 31 73 55 79 14 29 93 71 40 67 53 88 30 03 49 13 36 65
52 70 95 23 04 60 11 42 69 24 68 56 01 32 56 71 37 02 36 91
22 31 16 71 51 67 63 89 41 92 36 54 22 40 40 28 66 33 13 80
24 47 32 60 99 03 45 02 44 75 33 53 78 36 84 20 35 17 12 50
32 98 81 28 64 23 67 10 26 38 40 67 59 54 70 66 18 38 64 70
67 26 20 68 02 62 12 20 95 63 94 39 63 08 40 91 66 49 94 21
24 55 58 05 66 73 99 26 97 17 78 78 96 83 14 88 34 89 63 72
21 36 23 09 75 00 76 44 20 45 35 14 00 61 33 97 34 31 33 95
78 17 53 28 22 75 31 67 15 94 03 80 04 62 16 14 09 53 56 92
16 39 05 42 96 35 31 47 55 58 88 24 00 17 54 24 36 29 85 57
86 56 00 48 35 71 89 07 05 44 44 37 44 60 21 58 51 54 17 58
19 80 81 68 05 94 47 69 28 73 92 13 86 52 17 77 04 89 55 40
04 52 08 83 97 35 99 16 07 97 57 32 16 26 26 79 33 27 98 66
88 36 68 87 57 62 20 72 03 46 33 67 46 55 12 32 63 93 53 69
04 42 16 73 38 25 39 11 24 94 72 18 08 46 29 32 40 62 76 36
20 69 36 41 72 30 23 88 34 62 99 69 82 67 59 85 74 04 36 16
20 73 35 29 78 31 90 01 74 31 49 71 48 86 81 16 23 57 05 54
01 70 54 71 83 51 54 69 16 92 33 48 61 43 52 01 89 19 67 48";

my @rows;
foreach my $row (split(/\n/, $data)) { push @rows, [ split(/ /, $row) ] }

my $max = -1;
my $str_points = '';

sub compute4Points($$$$$$$$) { 
	my $val = $rows[$_[0]][$_[1]]*$rows[$_[2]][$_[3]]*$rows[$_[4]][$_[5]]*$rows[$_[6]][$_[7]];
	if ($val > $max) {$max = $val ;$str_points = join(',', @_);}
}

for(my $i = 0; $i < 20-3; $i++) {
	for(my $j = 0; $j < 20; $j++) {
		compute4Points($i, $j, $i+1, $j, $i+2, $j, $i+3, $j);
	}
}
for(my $i = 0; $i < 20; $i++) {
	for(my $j = 0; $j < 20-3; $j++) {
		compute4Points($i, $j, $i, $j+1, $i, $j+2, $i, $j+3);
	}
}
for(my $i = 0; $i < 20-3; $i++) {
	for(my $j = 0; $j < 20-3; $j++) {
		compute4Points($i, $j, $i+1, $j+1, $i+2, $j+2, $i+3, $j+3);
	}
}
for(my $i = 0; $i < 20-3; $i++) {
	for(my $j = 0; $j < 20-3; $j++) {
		compute4Points($i, $j+3, $i+1, $j+2, $i+2, $j+1, $i+3, $j);
	}
}

print "$max - ($str_points)";

```

## 12
```perl
my $sum = 1;
for (my $i = 2; ; $i++) {
	$sum += $i;
	my $nb_divisors = 2;
	for (my $j = 2; $j < sqrt($sum); $j++) {
		if ($sum % $j == 0) {
			$nb_divisors+=2;
			#print "$j;";
		}
	}
	print " - $i - $sum - (nb_divisors: $nb_divisors)\n" if ($i % 100 == 0);
	last if ($nb_divisors>=500);
}
print "$sum\n";
```
