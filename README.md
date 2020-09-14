# TestVocabulary
Công cụ này giúp bạn kiểm tra từ vựng do chính bạn để cập ra!

- Đây là code:
```php
<?php

class TestVocabularyEnglish {

	private $listvocabulary = [];
	
	public function enable(){
	    echo "version: 1.1\n"
	    echo "----- Danh sách lệnh -----\n";
	    echo "Thêm từ bằng cách .add\n";
		echo "Xóa từ bằng cách .delete\n";
		echo "Bắt đầu kiểm tra .start\n";
		echo "Kiểm tra từ vựng để kiểm tra trong danh sách .listvoc\n";
		echo "--------------------------\n";
		$this->openCommand();
	}
	
	public function clearChat(){
		echo "\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n";
	}
	
	public function openCommand(){
		fscanf(STDIN, "%s", $command);
		$this->typeCommands($command);
	}
	
	public function typeCommands(string $type){
		switch($type){
			case ".add":
				echo "Ghi 1 từ vựng(ví dụ: apple) (nếu bạn muốn cách thì để '_'):\n";
				fscanf(STDIN, "%s", $vocabulary);
				echo "Nghĩa của từ này là? (nếu bạn muốn cách thì để '_')\n";
				fscanf(STDIN, "%s", $mean);
                $this->listvocabulary[$mean] = $vocabulary;
				echo "Đã thêm từ thành công!\n";
				$this->clearChat();
				$this->openCommand();
			break;
			case ".delete":
				echo "Giờ hãy điền từ bạn cần xóa trong danh sách (nếu bạn muốn cách thì để '_'):\n";
				fscanf(STDIN, "%s", $delete);
				foreach($this->listvocabulary as $mean => $vocabulary){
					if($vocabulary === $delete){
						unset($this->listvocabulary[$mean]);
					}
				}				
				echo "Đã xóa từ thành công!\n";	
				$this->clearChat();
                $this->openCommand();					
			break;
			case ".start":
			    $this->clearChat();
				sleep(1);
				if(count($this->listvocabulary) <= 0){
					echo "Hết từ để kiểm tra!\n";
					break;
				}
				$vocabulary = array_rand($this->listvocabulary, 1);
				echo "Từ: ".$vocabulary." viết tiếng anh làm sao?\n";
				fscanf(STDIN, "%s", $type);
				$this->testing($type, $vocabulary);
			break;
			case ".listvoc":
                $this->showlistvocabulary();
			break;
			default: $this->openCommand();
		}
	}
	
	public function testing(string $type, string $vocabulary){	
        $this->clearChat();	
		if($type === $this->listvocabulary[$vocabulary]){
			echo "Đúng!\n";
			unset($this->listvocabulary[$vocabulary]);
		}
		else {
			echo "Sai!\n";
			unset($this->listvocabulary[$vocabulary]);
		}
		$this->clearChat();
		sleep(1);
		echo "Điền lệnh .start để bắt đầu kiểm tra tiếp!\n";		
		$this->openCommand();	
	}
	
	public function showlistvocabulary(){
		$this->clearChat();
		foreach($this->listvocabulary as $mean => $vocabulary){
			echo $vocabulary." => ".$mean."\n";
		}
		$this->openCommand();	
	}
}

$testVocabularyEnglish = new TestVocabularyEnglish();
$testVocabularyEnglish->enable();
```
