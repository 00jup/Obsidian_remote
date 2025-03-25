
핵심은 View에서 ViewModel을 수정하지 못하도록 하는 거임.

- **Model**: 앱의 데이터와 비즈니스 로직을 담당합니다.
    - 데이터 구조와 상태를 정의
    - 데이터 검증 로직 포함
    - 네트워크 요청이나 데이터베이스 작업과 같은 데이터 처리 담당
- **View**: 사용자 인터페이스를 담당합니다.
    - UIKit의 `UIViewController` 또는 SwiftUI의 `View`
    - 사용자의 입력을 받고 ViewModel에 전달
    - ViewModel의 데이터를 화면에 표시
- **ViewModel**: Model과 View 사이의 중재자 역할을 합니다.
    - View에서 사용할 수 있는 형태로 Model 데이터 변환
    - View에서 오는 사용자 입력을 처리
    - 상태 변경을 View에 알림 (바인딩)

```swift
// MARK: - Model
// 데이터와 비즈니스 로직을 담당
struct User {
    let id: Int
    let name: String
    let email: String
    let isPremium: Bool
}

// MARK: - ViewModel
// Model과 View 사이의 중간 계층, 비즈니스 로직 처리와 View에 데이터 제공
class UserViewModel {
    // 관찰 가능한 속성들
    private(set) var userName = Observable<String>("")
    private(set) var userEmail = Observable<String>("")
    private(set) var premiumBadgeHidden = Observable<Bool>(true)
    
    // 유저 모델
    private var user: User?
    
    // 서비스에서 유저 데이터 가져오기
    func fetchUser() {
        // 실제로는 네트워크나 데이터베이스에서 데이터를 가져옵니다
        // 여기서는 예시를 위해 하드코딩
        let user = User(id: 1, name: "홍길동", email: "hong@example.com", isPremium: true)
        self.user = user
        
        // Model -> ViewModel -> View 데이터 흐름
        updateUserInfo()
    }
    
    private func updateUserInfo() {
        guard let user = user else { return }
        
        userName.value = user.name
        userEmail.value = user.email
        premiumBadgeHidden.value = !user.isPremium
    }
    
    // 사용자 상태 변경 예시
    func togglePremiumStatus() {
        guard var user = user else { return }
        
        // 실제로는 API 호출이나 데이터베이스 업데이트를 수행합니다
        user = User(id: user.id, name: user.name, email: user.email, isPremium: !user.isPremium)
        self.user = user
        
        // View에 변경 내용 알림
        updateUserInfo()
    }
}

// 관찰 가능한 속성을 위한 Observable 클래스
class Observable<T> {
    var value: T {
        didSet {
            listener?(value)
        }
    }
    
    private var listener: ((T) -> Void)?
    
    init(_ value: T) {
        self.value = value
    }
    
    func bind(_ listener: @escaping (T) -> Void) {
        self.listener = listener
        listener(value)
    }
}

// MARK: - View
// UIKit 예시
import UIKit

class UserProfileViewController: UIViewController {
    // UI 요소들
    private let nameLabel = UILabel()
    private let emailLabel = UILabel()
    private let premiumBadge = UIImageView()
    private let toggleButton = UIButton()
    
    // ViewModel
    private let viewModel = UserViewModel()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
        bindViewModel()
        
        // 데이터 로드
        viewModel.fetchUser()
    }
    
    private func setupUI() {
        view.backgroundColor = .white
        
        // 이름 라벨 설정
        nameLabel.translatesAutoresizingMaskIntoConstraints = false
        nameLabel.font = UIFont.boldSystemFont(ofSize: 20)
        view.addSubview(nameLabel)
        
        // 이메일 라벨 설정
        emailLabel.translatesAutoresizingMaskIntoConstraints = false
        emailLabel.font = UIFont.systemFont(ofSize: 16)
        emailLabel.textColor = .gray
        view.addSubview(emailLabel)
        
        // 프리미엄 배지 설정
        premiumBadge.translatesAutoresizingMaskIntoConstraints = false
        premiumBadge.image = UIImage(systemName: "star.fill")
        premiumBadge.tintColor = .systemYellow
        view.addSubview(premiumBadge)
        
        // 토글 버튼 설정
        toggleButton.translatesAutoresizingMaskIntoConstraints = false
        toggleButton.setTitle("프리미엄 상태 변경", for: .normal)
        toggleButton.backgroundColor = .systemBlue
        toggleButton.layer.cornerRadius = 8
        toggleButton.addTarget(self, action: #selector(toggleButtonTapped), for: .touchUpInside)
        view.addSubview(toggleButton)
        
        // Auto Layout 제약 조건
        NSLayoutConstraint.activate([
            nameLabel.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 20),
            nameLabel.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            
            emailLabel.topAnchor.constraint(equalTo: nameLabel.bottomAnchor, constant: 8),
            emailLabel.leadingAnchor.constraint(equalTo: nameLabel.leadingAnchor),
            
            premiumBadge.centerYAnchor.constraint(equalTo: nameLabel.centerYAnchor),
            premiumBadge.leadingAnchor.constraint(equalTo: nameLabel.trailingAnchor, constant: 8),
            premiumBadge.widthAnchor.constraint(equalToConstant: 20),
            premiumBadge.heightAnchor.constraint(equalToConstant: 20),
            
            toggleButton.topAnchor.constraint(equalTo: emailLabel.bottomAnchor, constant: 20),
            toggleButton.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
            toggleButton.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20),
            toggleButton.heightAnchor.constraint(equalToConstant: 44)
        ])
    }
    
    private func bindViewModel() {
        // ViewModel의 Observable 속성들을 View의 UI 요소에 바인딩
        viewModel.userName.bind { [weak self] name in
            self?.nameLabel.text = name
        }
        
        viewModel.userEmail.bind { [weak self] email in
            self?.emailLabel.text = email
        }
        
        viewModel.premiumBadgeHidden.bind { [weak self] isHidden in
            self?.premiumBadge.isHidden = isHidden
        }
    }
    
    @objc private func toggleButtonTapped() {
        viewModel.togglePremiumStatus()
    }
}

// SwiftUI 예시
import SwiftUI
import Combine

// SwiftUI에서 사용할 ViewModel (ObservableObject 사용)
class UserViewModelSwiftUI: ObservableObject {
    @Published var name: String = ""
    @Published var email: String = ""
    @Published var isPremium: Bool = false
    
    private var user: User?
    
    func fetchUser() {
        let user = User(id: 1, name: "홍길동", email: "hong@example.com", isPremium: true)
        self.user = user
        
        updateUserInfo()
    }
    
    private func updateUserInfo() {
        guard let user = user else { return }
        
        name = user.name
        email = user.email
        isPremium = user.isPremium
    }
    
    func togglePremiumStatus() {
        guard var user = user else { return }
        
        user = User(id: user.id, name: user.name, email: user.email, isPremium: !user.isPremium)
        self.user = user
        
        updateUserInfo()
    }
}

// SwiftUI View
struct UserProfileView: View {
    @ObservedObject var viewModel = UserViewModelSwiftUI()
    
    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            HStack {
                Text(viewModel.name)
                    .font(.title)
                    .bold()
                
                if viewModel.isPremium {
                    Image(systemName: "star.fill")
                        .foregroundColor(.yellow)
                }
            }
            
            Text(viewModel.email)
                .font(.subheadline)
                .foregroundColor(.gray)
            
            Button(action: {
                viewModel.togglePremiumStatus()
            }) {
                Text("프리미엄 상태 변경")
                    .frame(maxWidth: .infinity)
                    .padding()
                    .background(Color.blue)
                    .foregroundColor(.white)
                    .cornerRadius(8)
            }
            .padding(.top, 20)
        }
        .padding()
        .onAppear {
            viewModel.fetchUser()
        }
    }
}

// 사용 예시
struct ContentView: View {
    var body: some View {
        UserProfileView()
    }
}
```