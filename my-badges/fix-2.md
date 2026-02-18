<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/cloudlab/commit/3e76ced43286fd63cd36af6f477c1fc551de2d72">3e76ced</a>: Fix permission issue when creating deployment directory

- Use sudo to create /opt/cloudlab directory structure
- Set ownership to deployment user after creation
- Fixes 'Permission denied' error when deploying
- <a href="https://github.com/ksysoev/cloudlab/commit/0c4e80a68eb68665baac8102707aa6bcc2ca1c1a">0c4e80a</a>: Fix tr command syntax error in service name sanitization

Changed 'tr - '''  to 'tr -d '-'' to properly delete hyphens.
The empty string as second argument to tr was causing failure.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>