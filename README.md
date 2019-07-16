# MAYA_MEL
MEL Scripts used in R&D/Production

## Velocity (Feather Generator)

Locator -> Custom attribute "speed" expression

```
float $lastPosX = `getAttr -t (frame-1) featherRig.tx`;
float $lastPosY = `getAttr -t (frame-1) featherRig.ty`;
float $lastPosZ = `getAttr -t (frame-1) featherRig.tz`;

featherRig.speed = abs (mag (<<featherRig.translateX,featherRig.translateY,featherRig.translateZ>>)- mag (<<$lastPosX,$lastPosY,$lastPosZ>>) );

if (featherRig.speed > 10){
	emitter1.rate =10;
};
```

feather_nParticleShape creation expression

```
feather_nParticleShape.randomID = rand(0,2);

int $rndX=rand(360);
int $rndY=rand(360);
int $rndZ=rand(360);
float $scale = rand(0.25,1);

feather_nParticleShape.rotationPP = <<$rndX,$rndY,$rndZ>>;
feather_nParticleShape.scalePP = <<$scale,$scale,$scale>>;
```

feather_nParticleShape runtime before dynamics expression

```
vector $rot = feather_nParticleShape.rotationPP;
vector $v = feather_nParticleShape.velocity;

float $rX;
float $rY;
float $rZ;

if ($v.x != 0){
	if ($rot.x > 0){
		$rX = $rot.x - 5;
		$rY = $rot.y - 1;
	}
	else
	{
		$rX = $rot.x;
		$rY = $rot.y + rand(5,25);	
	};

	if ($rot.z > 0){
		$rZ = $rot.z - 5;
	};
}
else
{
	$rX = 0;
	$rY = $rot.y;
	$rZ = 0;
};

feather_nParticleShape.rotationPP = <<$rX, $rY,$rZ>>;
```
