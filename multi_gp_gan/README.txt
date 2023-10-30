1. make_list_path.py를 실행하여 원하는 디렉토리에 대해 먼저 target.csv파일 만들기
-bg_dir: background들이 저장된 directory
-src_dir: merge할 사진이 있는 directory
2. target.csv가 만들어진 후에! src_dir에서 make_mask_cur 실행, 자동으로 원래이름_mask.png 파일이 만들어짐
3. python run_gp_gan_list.py --list_path "target.csv위치/target.csv" --result_folder "원하는 폴더"
--generator_path "./train1201/GP-GAN_2021-12-01-10-08-58.ckpt-5168595004"

를 행하면 원래의 파일과 같은 이름으로 gpgan된 이미지가 만들어짐 이후에 src dir에서 .txt 파일만 복사하여
blended result가 있는 위치로 붙여넣으면 됨!